# Fertility Clinic Booking Appointments

We want to launch a booking facility with partner clinics.

We will provide JSON which represents all time slots for a given day across multiple clinics. The data is in this format:

```typescript
interface Appointment {
    clinicId: string;
    clinicName: string;
    startTime: string;
    endTime: string;
    booked: boolean;
    patientName?: string;
}
```

e.g.

```json
{
    "clinicId": "1",
    "clinicName": "Aurora Reproductive Healthcare",
    "startTime": "2024-03-29T11:30:00Z",
    "endTime": "2024-03-29T12:00:00Z",
    "booked": true,
    "patientName": "Zou Jian"
}
```

We’d like you to use the JSON to complete the following exercises.

## Setup

You can use whatever language you are most comfortable in. 

You will need to be able to load a JSON file and print text to the screen only.

## Task 1: Print out the percentage availability for the clinics

Print out the availability at each clinic. An appointment is booked if `booked: true` is set in the JSON. E.g.

```
Spire Healthcare Limited: 25%
Apricity Fertility: 10%
```

## Task 2: Move patients due to emergency appointment

Sometimes an emergency appointment will be booked on the same day as existing appointments, and a clinic may need to move patients to a different clinic or suggest a later appointment. This may affect multiple patients.

The clinic would like a list of which appointments can be moved.

The function signature for this can be shown like so:

```typescript
function suggestNewAppointments(
    appointments: Appointment[],
    clinicId: number,

    // ISO 8601
    emergencyAppointmentStart: string,
    emergencyAppointmentEnd: string,

    // The acceptable amount of time the appointment can change by
    toleranceMinutes: number
): string {}
```

It should output a set of move instructions for clinic staff, e.g:

```
1. Move patient “Zou Jian” to 11:10 @ “Spire Healthcare Limited" (20 minutes earlier)
2. Move patient “Brian Hamilton” to 13:10 @ “Spire Healthcare Limited” (40 minutes later)
3. Patient “Brian Hamilton” could not be accommodated.
```

Notes:
- A patient can be moved to a different clinic.
- The “tolerance” allows for an earlier or later appointment.
- If there are no other suitable appointments, the output should state that.
