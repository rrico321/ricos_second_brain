<%*
const desc = await tp.system.prompt("Task description");
const due = await tp.system.prompt("Due date (YYYY-MM-DD), leave blank if none");
if (due && due.trim() !== "") {
  tR += `- [ ] ${desc} ➕ ${tp.date.now("YYYY-MM-DD")} 📅 ${due.trim()}`;
} else {
  tR += `- [ ] ${desc} ➕ ${tp.date.now("YYYY-MM-DD")}`;
}
%>
