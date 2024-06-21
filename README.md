# 💕 What is Winkie? ༊*·˚
Winkie is a strategic and cute board game, to play with your friends!!! This repo is for allowing players to add game modes to Winkie, just fork it and do the changes you want to do! I hope you will enjoy! (,,>﹏<,,)

### **Links!** <br/>
╰┈➤ ~[Play Winkie]()~ <br/>
╰┈➤ [Join To Community](https://discord.gg/XDWyeekEFY)

## 🎀 How does mods works?

In Winkie you can create a room by a post request. `/room/room-create` does it with the required request body...

<table>
<tr>
<th>Request</th>
<th>Response</th>
</tr>
<tr>
<td>
  
```json
{
  "room_name": "Kui's lovely room",
  "room_pswd": "passOwOrd",
  "room_mode": "casual"
}
```

</td>
<td>

```json
{
  "id": "1718882906488",
  "owner": "192.158.1.38",
  "name": "Kui's lovely room",
  "password": "passOwOrd",
  "mode": "casual",
  "teams": ["white", "black"],
  "clients": [],
  "board": {
    "2;7": { "piece": "capple", "team": "white" },
    "8;0": { "piece": "capple", "team": "black" }
  }
}
```

</td>
</tr>
</table>

Server returns with this data, because there is a subfolder named "casual" in mods. And it contains `data.yml` file that looks like this:
```yml
---
game:
  teams:
    - white # First team
    - black # Second team
# First player joins to first team and the second player joins to second team, if a third person joins too their team will be set as "spectator" :3
board:
  size  : 7 # Define the board size!!
# If you set it as 7, you will see 7 big squares, which means 225 playable square!! because of Winkie's perfect rules OwO (The formula is (2n+1)^2 if you want to calculate)
  layout:
    2;7 : { piece: capple, team: white } # 2;7 is a coordinate that means x: 2, y: 7, and it defines which piece will be placed on that square on which team!! ^-^
    8;0 : { piece: capple, team: black }
# Note: Board origin is at the top-left of board and it's position is "0;0" \(^ω^\ )
piece: 
  capple: # Create a piece object and give it a name!
    piece_name : Lovely Capple # It's also a name but symbols are allowed.. So you can *ੈ✩‧₊˚༺ ժׁׅ݊ ꫀׁׅܻ ᝯׁ ᨵׁׅ ꭈׁׅ ɑׁׅ֮ tׁׅ ꫀׁׅܻ ༻*ੈ✩‧₊˚ the name!
    effects:
      immortal: false # The other pieces won't be able to take this piece when this setting is set to true!
      glutonny: false # This piece will be able take the pieces which is from the same team with it when this setting set to true! (Don't ask why, it sounds like a good feature U⩊U)
      ghost   : false # This piece will be able to jump over other pieces when this setting set to true!
      psycho  : false # When it's true and if you take the opponent's piece with this piece, it will be your turn again. But you can only move the same piece (It repeats itself)!!
    movement:
# x means horizontal position, y means vertical position, d means distance and works like repeat count, b means block it or not, s means skip! Let me give you some examples!! ^-^
# Note: 3 points equals to 1 square!
      regular: # Regular moves of piece:
        - {x: +1, y: +1, d: .inf} # This means, the piece can move diagonal to top-right with no limits!
        - {x: +1, y: +1, d: 5} # The piece can move diagonal to top-right with for first 5 square!

        - {x: 0, y: +3, d: 1} # The piece can move to 3rd point above of it!
        - {x: 0, y: +3, d: 2} # The piece can move to 3rd and 6th point above of it!
        - {x: 0, y: +3, d: 3} # The piece can move to 3rd, 6th and 9th point above of it!

        - {x: 0, y: +2, d: .inf} # If we start counting the points that above the piece, the piece will able to move only even numbers that we counted.
        - {x: 0, y: +1, s: 2, d: .inf} # If we start counting the points that above the piece, the piece will able to move only odd numbers that we counted.

        - {x: +1, y:  0, d: 1, b: true} # The piece wouldn't be able to move 1 point right.
        - {x:  0, y: +1, d: 1, b: true} # The piece wouldn't be able to move 1 point above.

# Note: Skipping points doesn't means you can jump over them like the knight from chess! You need to set true the "ghost" from the effects if you want to jump over them. (¬_¬")
# Example: Let's say your piece is on 5;0 and the opponent piece is on 4;0 your regular movements contains {x: -2, y: 0, d: .inf} You can't be able to move to 3;0 because eney will block the path!  
      
      capture: # The piece will be allowed to move theese points when the opponent piece is standing on them... TO DESTROY THEM!!! (˶ˆ꒳ˆ˵)
        - {x: +1, y:  0, d: .inf} # The piece can take any piece on right side.
        - {x: -1, y:  0, d: .inf} # The piece can take any piece on left side.

      corner: # When you are not in the middle of a square, your regular moves will be blocked and this moves will be allowed.
        - {x: 0, y: +1, d: .inf} # The piece can move to any point on above of it!
        - {x: 0, y: -1, d: .inf} # The piece can move to any point down of it!

      opening: # This path will be an option when you are about to make the first move wtih this piece! Just like moving 2 squares on first move with pawns. 
        - {x: 0, y: +1, d: 3} # The piece can move 3 points above of it on first move.

    reactions: # I am having issues with this feature, i will add it soon... T-T
```

You can edit this Yaml file and send a pull request to play with your friends, I will edit it if it needs but also i will make sure i give credit to you!! ^-^
Oh, a mod folder also includes a subfolder named "resources" it has the assets of the pieces!

```
mods
   ├── casual
   │        ├── resources
   │        │           ├── white
   │        │           │       └── capple.png
   │        │           └── black
   │        │                   └── capple.png
   │        └── data.yml
   ├── huge-board
   └── chess
```
So don't forget to add the assets of your pieces while forking this repo!
I love y'all <3
