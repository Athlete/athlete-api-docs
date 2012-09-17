ChangeLog
=========

**September 17**

- Changed API method for marking a conversation as read. Changed from PATCH to POST, removed unnecessary ID argument,
  and accept an ID of the last messsage read in that conversation (to check for conflicts) instead of a date.

**September 12**

- Change user password
- Route object includes "is_favorite"
- Update favorite status of a route 

**September 11**

- Friendship exists method
- We changed the way to specify a user location. Check out profile docs.

**September 9**

- Share a workout. Check out workout docs.

**September 6**

- Added facebook token to the workout. You can provide the token to share the workout in facebook. Check Workouts docs.

**August 30**
- Deprecated PATCH method on Workouts
- Added privacy to GPX representation for workouts (check workouts docs)

**August 2**
- Changed ordering for conversations. See "GET /conversations/".

**July 11**

- Added "privacy" to workout resource.
- static_map_url will sometimes be missing from workout resource if the user does not have privileges to see it.
- Added null to Posts pagination when the last page is reached.

**June 15**

- Removed facebook registration. facebook login now performs both login and registration.
- Fixed docs. To update the profile picture the correct path is /user/picture/

**June 6**

- All times from the API are now in UTC timezone. We previously had some timezone issues.

**May 29**

- **IMPORTANT** Changed parameters on Post resource. The way to specify a user changed, from "user" to "user_id". Take a look at Post resource docs.
- Added profile type for posts. You can get a user's profile feed specifying the profile type and user_id.
- Added Back to first_name and last_name in User Resource
- Removed full_name from User Resource
- Added likers to comment list response

**May 28**

- Added post filters for comments.
- MD5 content fully tested. You can upload profile pics now.
- Updated comment POST.
- Updated docs: Comment, User.
