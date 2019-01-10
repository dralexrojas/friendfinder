# Friend Finder - Node and Express Servers

### Overview
Build a compatibility-based "FriendFinder" application -- basically a dating app. This full-stack site takes in results from users' surveys, then compares their answers with those from other users (existing users). The app will then display the name and picture of the existing user with the best overall match to the new user.

PP Friend Finder: https://ppfriendfinder.herokuapp.com/

---
### Folder/File Structure 
```
  FriendFinder
    - .gitignore
    - app
      - data
        - friends.js
      - public
        - home.html
        - survey.html
      - routing
        - apiRoutes.js
        - htmlRoutes.js
    - node_modules
    - package.json
    - server.js
```
---
### Code Screenshots (sample)

* Catch-all route that leads to `home.html` which displays the home page.
```javascript
app.get("/", function(req, res) {
        res.sendFile(path.join(__dirname, "../public/home.html"));
});
```

* GET Route to `/survey` which should display the survey page.
```javascript
app.get("/survey", function(req, res) {
        res.sendFile(path.join(__dirname, "../public/survey.html"));
});
```

* GET route with the url `/api/friends`. This will be used to display a JSON of all possible friends.
```javascript
app.get("/api/friends", function(req, res) {
        res.json(friends);
});
```

* User data saved inside of `app/data/friends.js` as an array of objects.
```json
var friends = [
    {
        "name": "Steven Patrick Morrissey",
        "photo": "https://www.biography.com/.image/ar_1:1%2Cc_fill%2Ccs_srgb%2Cg_face%2Cq_auto:good%2Cw_300/MTE5NTU2MzE2NjYyMTA1NjEx/photo-of-morrissey-and-smiths.jpg",
        "scores": ["2", "2", "2", "2", "2", "2", "2", "2", "2", "2"]
    },
    {
        "name": "Sheryl Crow",
        "photo": "https://s3.amazonaws.com/system.ravinia.org/shows/899/3754_Show_Page.jpg",
        "scores": ["3", "3", "3", "3", "3", "3", "3", "3", "3", "3"]
    }
    ];
```

* POST routes `/api/friends`. This will be used to handle incoming survey results and the compatibility logic.
```javascript
app.post("/api/friends", function(req, res) {
        
        var difference = 40;
        var matchName = "";
        var matchPhoto = "";
...
// Loop and User Input logic/match calculation.......(not included here)
...
        res.json({
            name: matchName,
            photo: matchPhoto
        });

        friends.push(req.body);
});
```
---