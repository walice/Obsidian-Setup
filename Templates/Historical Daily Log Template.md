<%* 
// Parse and clean the file
let lines = tp.file.content.split('\n');

// Remove any H1 header (line starts with "# ")
lines = lines.filter(line => !line.startsWith('# '));

// Trim leading blank lines
while (lines.length > 0 && lines[0].trim() === '') {
  lines.shift();
}

// Prepare content block
let cleaned = lines.join('\n');

// Extract date from filename
let date = moment(tp.file.title.substring(0, 10), "YYYY-MM-DD");
let header = `# ${date.format("dddd MMMM DD")}`;

// Generate yesterday/tomorrow links
let yesterday = date.clone().subtract(1, "days");
let tomorrow = date.clone().add(1, "days");

let yesterdayPath = `Daily Logs/${yesterday.format("YYYY")}/${yesterday.format("MM-MMMM")}/${yesterday.format("YYYY-MM-DD-ddd")}`;
let tomorrowPath = `Daily Logs/${tomorrow.format("YYYY")}/${tomorrow.format("MM-MMMM")}/${tomorrow.format("YYYY-MM-DD-ddd")}`;

let nav = `📅 [[${yesterdayPath}|Yesterday]] | [[${tomorrowPath}|Tomorrow]]`;

// Final output with exactly one blank line between nav and bullets
tR = `${header}\n\n${nav}\n\n${cleaned}`;
%>
