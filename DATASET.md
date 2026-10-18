# Dataset contract

The JSON file is a constructed benchmark, not an export of an institutional system. No student names or named lecturers are included.

| Field | Definition |
| --- | --- |
| `schema_version` | Integer 1 |
| `calendar.days` | Unique ordered day names; default Monday through Saturday |
| `calendar.day_start`, `day_end` | HH:MM day bounds |
| `calendar.breaks` | Protected `[start, end]` HH:MM intervals |
| `calendar.slots` | Ordered, nonoverlapping one-hour `[start,end]` intervals excluding breaks |
| `modules` | Module code to supplied title mapping |
| `cohorts` | Unique ID, positive size, programme/year/section, off_days and provisional flag |
| `lecturers` | Unique ID and optional unavailable list |
| `rooms` | Unique ID, type, positive capacity and optional unavailable list |
| `events` | Unique ID, cohort, module, lecturer and required room_type |

Availability entries are `[day_name, zero_based_slot_index]`, for example `["Monday", 0]` means unavailable Monday 09:30–10:30 in the default calendar. The lunch interval is not a slot.

Output assignments use event IDs plus a flattened time index and a zero-based room index. `time = day_index * number_of_teaching_slots + slot_index`. The exported CSV converts indices into readable day, time, room and lecturer IDs. Do not modify the ordering of an instance's rooms while reusing an old index-based assignment; validate against the exact input snapshot accompanying that assignment.

## Change the workload

To change weekly contact hours, add or remove event rows while preserving unique event IDs. Each module offering currently has three events. To appoint different lecturers to different sections, add lecturer records and change the relevant events' lecturer IDs. To combine lectures across cohorts requires a multi-cohort attendance extension; do not represent the merged lecture as two simultaneous events in one room.

The one-hour model does not enforce contiguous hours. For any two-hour practical that must remain uninterrupted, extend the occupancy model rather than merely duplicating an event.

## Original cohort off days

| Cohort | Off days |
| --- | --- |
| CS2 | Thursday, Saturday |
| SE1 | Wednesday, Friday |
| DS2A and DS2B | Tuesday, Friday |
| SE2A | Monday, Thursday |
| SE2B | Thursday, Saturday |
| SE3A | Tuesday, Thursday |
| SE3B | Tuesday, Saturday |
| SE3C | Thursday, Friday |
| DS3A | Wednesday, Saturday |
| DS3B | Monday, Tuesday |
| CS4 and SE4 | Thursday, Friday, Saturday |
| DS4 | Tuesday, Wednesday, Friday |
| CS3 and SE3SQA | No off days provisionally; six-day availability explicitly approved for this benchmark |

There are 509 synthetic students, 18 synthetic lecturers and eight synthetic rooms in the reference instance. All five lecture rooms seat 45 and three labs seat 40. The 50 offerings produce 107 lecture-type and 43 lab meetings. Do not describe these as actual institutional resource allocations.
