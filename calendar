#!/usr/bin/env python3

from icalendar import Calendar, Event
import requests
import argparse

parser = argparse.ArgumentParser()

parser.add_argument('-u', '--url', required=True, help='URL of the ics file')
parser.add_argument('-o', '--outputfolder', type=str, required=True, help='Path to File, e.g. C:\\output\\result.ics')

args = parser.parse_args()

ics = requests.get(args.url).text
if "SUBCALENDAR_NOT_FOUND" in ics:
  print("SUBCALENDAR_NOT_FOUND")
  exit(1)
gcal = Calendar.from_ical(ics)
for component in gcal.walk():
  if component.get("summary"):
    component["summary"] = "belegt"
  if component.get("description"):
    component["description"] = ""
f = open(args.outputfolder, "wb")
f.write(gcal.to_ical())
f.close()
exit(0)
