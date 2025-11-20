<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Slice & Sip Par-3 League</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Roboto', sans-serif; margin:0; padding:0; background:#f0f4f8; color:#333;}
    header { background: linear-gradient(90deg,#1e3a8a,#3b82f6); color: #fff; padding:40px 20px; text-align:center;}
    header h1 { font-size:2.8em; margin:0;}
    header p { margin:5px 0 0 0; font-size:1.2em; }
    .container { max-width: 1000px; margin:auto; padding:20px; }

    .section { background: #fff; border-radius:12px; padding:20px; margin-bottom:25px; box-shadow: 0 4px 15px rgba(0,0,0,0.1);}
    h2 { text-align:center; margin-bottom:15px; color:#1e3a8a;}

    table { width:100%; border-collapse: collapse; margin-top:10px;}
    th, td { padding:12px 8px; text-align:left; border-bottom:1px solid #e0e0e0;}
    th { background:#1e3a8a; color:#fff; font-weight:700;}
    tr:hover { background:#f5f5f5; }
    .gold { background: #ffd700 !important; color:#000; font-weight:700;}
    .silver { background: #c0c0c0 !important; color:#000; font-weight:700;}
    .bronze { background: #cd7f32 !important; color:#fff; font-weight:700;}

    .team-card { background:#e0e7ff; padding:15px 20px; border-radius:10px; margin-bottom:15px; transition:transform 0.2s;}
    .team-card:hover { transform: scale(1.03);}
    .team-name { font-weight:700; font-size:1.3rem; margin-bottom:8px; color:#1e3a8a;}
    .roster-name { margin-left:15px;}

    .updated { font-size:0.9em; text-align:right; color:#555; margin-top:5px;}
    @media(max-width:600px){ th, td{ font-size:14px; padding:8px 5px;} header h1{ font-size:2em;} }
  </style>
</head>
<body>

<header>
  <h1>Slice & Sip Par-3 League</h1>
  <p>Weekly Standings, Scores, Schedule & Teams</p>
</header>

<div class="container">
  <!-- Standings -->
  <div class="section">
    <h2>Standings</h2>
    <div id="standings">Loading...</div>
    <div id="standings-updated" class="updated"></div>
  </div>

  <!-- Weekly Scores -->
  <div class="section">
    <h2>Weekly Scores</h2>
    <div id="scores">Loading...</div>
    <div id="scores-updated" class="updated"></div>
  </div>

  <!-- Schedule -->
  <div class="section">
    <h2>Schedule</h2>
    <div id="schedule">Loading...</div>
    <div id="schedule-updated" class="updated"></div>
  </div>

  <!-- Teams & Rosters -->
  <div class="section">
    <h2>Teams & Rosters</h2>
    <div id="teams">Loading...</div>
    <div id="teams-updated" class="updated"></div>
  </div>
</div>

<script>
const SHEET_ID = "1LSXpUUwyDJ1KZV6U-7mvd7WPszWRP8-rMGVRpgw67qw";
const STANDINGS_URL = `https://opensheet.elk.sh/${SHEET_ID}/Standings`;
const SCORES_URL    = `https://opensheet.elk.sh/${SHEET_ID}/Scores`;
const SCHEDULE_URL  = `https://opensheet.elk.sh/${SHEET_ID}/Schedule`;
const TEAMS_URL     = `https://opensheet.elk.sh/${SHEET_ID}/Teams`;

/* Utility for Last Updated */
function showUpdated(elementId){
  const now = new Date();
  document.getElementById(elementId).textContent = "Last updated: " + now.toLocaleString();
}

/* Load Standings with Top 3 Highlights */
async function loadStandings(){
  const data = await fetch(STANDINGS_URL + `?t=${Date.now()}`).then(r=>r.json());
  let html = "<table><tr><th>Team</th><th>Points</th><th>Total Score</th></tr>";
  data.forEach((row,index)=>{
    let className="";
    if(index===0) className="gold";
    else if(index===1) className="silver";
    else if(index===2) className="bronze";
    html += `<tr class="${className}"><td>Team ${index+1}</td><td>${row.Points}</td><td>${row.TotalScore}</td></tr>`;
  });
  html += "</table>";
  document.getElementById("standings").innerHTML = html;
  showUpdated("standings-updated");
}

/* Load Scores */
async function loadScores(){
  const data = await fetch(SCORES_URL + `?t=${Date.now()}`).then(r=>r.json());
  let html = "<table><tr><th>Week</th><th>Team</th><th>Score</th><th>Points</th></tr>";
  data.forEach(row=>{
    html += `<tr><td>${row.Week}</td><td>${row.Team}</td><td>${row.Score}</td><td>${row.Points}</td></tr>`;
  });
  html += "</table>";
  document.getElementById("scores").innerHTML = html;
  showUpdated("scores-updated");
}

/* Load Schedule */
async function loadSchedule(){
  const data = await fetch(SCHEDULE_URL + `?t=${Date.now()}`).then(r=>r.json());
  let html = "<table><tr><th>Week</th><th>Date</th><th>Matchup</th></tr>";
  data.forEach(row=>{
    html += `<tr><td>${row.Week}</td><td>${row.Date}</td><td>${row.Matchup}</td></tr>`;
  });
  html += "</table>";
  document.getElementById("schedule").innerHTML = html;
  showUpdated("schedule-updated");
}

/* Load Teams */
async function loadTeams(){
  const data = await fetch(TEAMS_URL + `?t=${Date.now()}`).then(r=>r.json());
  let teams={};
  data.forEach(row=>{
    if(!teams[row.Team]) teams[row.Team]=[];
    teams[row.Team].push(row.Player);
  });
  let html="";
  Object.keys(teams).forEach((teamKey,index)=>{
    html += `<div class="team-card"><div class="team-name">Team ${index+1}</div>`;
    html += teams[teamKey].map(p=>`<div class="roster-name">• ${p}</div>`).join("");
    html += "</div>";
  });
  document.getElementById("teams").innerHTML = html;
  showUpdated("teams-updated");
}

/* Load All Sections */
loadStandings();
loadScores();
loadSchedule();
loadTeams();
</script>

</body>
</html>
