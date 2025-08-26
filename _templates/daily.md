<%*
const year = tp.date.now("YYYY");
const month = tp.date.now("MM");
const folder = `일일기록/${year}/${month}`;
await tp.file.move(`${folder}/${tp.date.now("YYYY-MM-DD")}`);
%>

