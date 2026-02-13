# RSS Feed Filter with Trigger System

A news feed filtering application with a deep OOP inheritance hierarchy implementing strategy and composite design patterns. Includes phrase, time, and logical triggers that compose into complex filter rules, a configuration file parser, and a Tkinter GUI that polls RSS feeds on a background thread.

## Implementation

### Data Model

`NewsStory` — data class with guid, title, description, link, and publication date.

### Trigger Hierarchy

- `Trigger` — abstract base class defining the `evaluate()` interface
- `PhraseTrigger(Trigger)` — `is_phrase_in()` normalizes text (replaces punctuation with spaces, lowercases, splits and rejoins) and checks for consecutive word phrase matching
- `TitleTrigger(PhraseTrigger)` — fires when the title contains the phrase
- `DescriptionTrigger(PhraseTrigger)` — fires when the description contains the phrase
- `TimeTrigger(Trigger)` — parses date strings to datetime with EST timezone
- `BeforeTrigger(TimeTrigger)` / `AfterTrigger(TimeTrigger)` — fire based on publication date comparison
- `NotTrigger(Trigger)` — inverts another trigger
- `AndTrigger(Trigger)` — logical AND of two triggers
- `OrTrigger(Trigger)` — logical OR of two triggers

### Filtering and Configuration

- `filter_stories()` — filters a list of stories, keeping any story that fires at least one trigger
- `read_trigger_config()` — parses a trigger configuration file to build trigger objects declaratively

### GUI

`main_thread()` — Tkinter GUI that polls Google/Yahoo RSS feeds every 120 seconds on a background thread and displays filtered stories.
