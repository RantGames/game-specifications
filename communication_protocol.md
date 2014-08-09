# Move

Property | Type | Information
----------- | ------- | ---------------
action    | String | Type of move. Currently supported types are 'attack_unit' and 'move_unit'
origin_city_id | Integer | 
target_city_id | Integer | 
quantity | Integer | Number of units to send from origin to target

# Game

Property | Type | Information
----------- | ------- | ---------------
id    | Integer | Unique id for this game
winner | String | Name of winning player, or null if no player has won yet
players | List of Player| List of Player objects in current game

# Player

Property | Type | Information
----------- | ------- | ---------------
user_id    | Integer | Unique id for this player
gravatar_hash | String | 
name | String | Player displayname 
cities | List of City | List of City objects that belong to player

# City

Property | Type | Information
----------- | ------- | ---------------
id | Integer | Uniquie id for this city
name    | String | 
latitude | Double | 
longitude | Double |
units | Integer | quantity of units in this city

# HTTP Endpoints

game/new - If current session is not in a game, create new game and assign current session to it. If player is in game return HTTP 403

game/move - Takes Move as POST data. Validates turn against game rules and if valid saves it to storage. If this is the last Move to be submitted, process current game turn. If player is not in a game return HTTP 403.

game/skip_turn - Skips current turn for current session, if they have not already. If they are the last player, process the current game turn. If player is not in a game return HTTP 403

game/current_player_id - Returns id of player object attached to current session. If no player is logged in return HTTP 404

game/current_state - Returns JSON representation of current game state if current session is in a game. Otherwise return HTTP 404
