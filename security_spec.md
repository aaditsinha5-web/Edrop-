# Security Specification - E-Drop

## Data Invariants
1. A Pickup must have a valid `userId` matching the authenticated user.
2. A User profile can only be created or modified by the owner.
3. Impact scores can only be incremented, never decremented by the user directly (controlled by validation).
4. Status changes are restricted to certain flows.

## The Dirty Dozen Payloads (Rejections)
1. Creating a pickup with another user's `userId`.
2. Updating someone else's pickup.
3. Increasing `impactScore` by a million points in one update.
4. Deleting a pickup (only cancellation allowed).
5. Setting `status` to 'completed' as a normal user (if that's admin only).
6. Creating a pickup without required fields.
7. Injecting huge strings into the `address` field.
8. Modifying `createdAt` time.
9. Reading all users' profiles.
10. Creating a user profile for a different UID.
11. Updating `email` to an unverified one without owner permission.
12. Listing pickups without filtering by `userId`.

## Test Runner (Conceptual)
Tests will verify that these payloads return PERMISSION_DENIED.
