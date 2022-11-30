# @notedwin/autocode-discordjs

## API Methods

### User class
```js
const {User} = require('@notedwin/autocode-discordjs');

//DISCLAIMER: user_id is self defined, no example will be given

let user = new User(user_id)
console.log(user)
/** Output:
 * User {
 *   id: '235721297244585984',
 *   bot: false,
 *   system: false,
 *   flags: [ 'HOUSE_BALANCE', 'ACTIVE_DEVELOPER' ],
 *   username: 'Edwin',
 *   discriminator: '8437',
 *   avatar: 'ace6668e3a4d0d33ba955e2b4341d97e'
 * }
*/

//fetch basic user informations
console.log(user.fetch(user_id))

//fetch user's Discord creation time
console.log(user.createdAt);
/** Output:
 * 2016-10-12T11:12:16.753Z
 */

//fetch the Discord unix timestamp of when the user was created
console.log(user.createdTimestamp);
/** Output:
 * 1476270736
 * 
 * How to use:
 * <t:${user.createdTimestamp}:R>
 */

//The hexadecimal version of the user accent color, with a leading hash
console.log(user.hexAccentColor);

//The Discord "tag" (e.g. "Edwin#8437") for this user
console.log(user.tag)
```

### Tools class
```js
const {Tools} = require('@notedwin/autocode-discordjs');

//DISCLAIMER: author is self defined, no examples will be given.

tools.getUserBadges(author.public_flags)
/** Same function were used to retrieve flags in User class which can be accessed through
 * 
 * let user = new User(author)
 * 
 * console.log(user.flags);
*/
```

## Example Usage For Autocode

### **Tools:** get user's publicly displayed badges like hypesquad badge, discord moderator badge, etc.

```js
let { User, Tools } = require('@notedwin/autocode-discordjs');

let message = context.params.event;

let user = new User(message.author);

Tools.getUserBadges(user.public_flags);
```

### **CreateChannel:** ability to use this class similar like Discord.js to create new channels, set parent (category), set position (position of the channel in a category), and send message to a specific channel.

```js
let { CreateChannel } = require('@notedwin/autocode-discordjs');

let message = context.params.event;

//channels.create(name, { guild_id, type, topic, bitrate, user_limit, rate_limit_per_user, position, permission_overwrites, parent_id, nsfw });
//bitrate and user_limit is only applicable for voice channels and stage channels.
//check out more about bitrates here by reading the * section: https://discord.com/developers/docs/resources/channel#modify-channel-json-params-guild-channel
//Check out more about channel type here: https://discord.com/developers/docs/resources/channel#channel-object-channel-types

let channel = new CreateChannel(message);

let createdChannel = await channel.create('test-channel', {
    type: 0, //for now, you will have to use the integer type from Discord Dev Portal. An alternative way is coming soon.
    topic: `channel topic here`, //optional
})

/** replace the data with the created channel's data if you wanna update the created channel's info.
 *  use the original context.params.event if you wanna update the current channel's info instead.
 */
channel = new CreateChannel(createdChannel)
await channel.setName('new-channel-name')
await channel.setParent('891309033884094525')
```
