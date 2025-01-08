

```dataviewjs
function getJsonLength(jsonData) {
    var length = 0;
    for (var ever in jsonData) {
        length++;
    }
    return length;
}

function getYMD(n) {
    var today = new Date();
    var targetday_milliseconds = today.getTime() + 1000 * 60 * 60 * 24 * n;
    today.setTime(targetday_milliseconds);
    var tYear = today.getFullYear();
    var tMonth = ("0" + (today.getMonth() + 1)).slice(-2);
    var tDate = ("0" + today.getDate()).slice(-2);
    return tYear + "-" + tMonth + "-" + tDate;
}

const jsonString = await app.vault.adapter.read(".obsidian/vault-stats.json");
const jsonObject = JSON.parse(jsonString);

const length = getJsonLength(jsonObject.history);
const YMD = [];
const ycount = [];
const data = [];

for (let i = 0; i < length; i++) {
    YMD.push(getYMD(0 - i));
    if (jsonObject.history[YMD[i]]) {
        ycount.push(jsonObject.history[YMD[i]].words);
    } else {
        ycount.push(0);
    }
    data.push([YMD[i], ycount[i]]);
}

const currentYear = new Date().getFullYear();

const option = {
    backgroundColor: "rgba(0, 0, 0, 0)",
    width: 650,
    height: 250,
    tooltip: {
        position: "top",
        trigger: "item",
        formatter: function (params) {
            let dataIndex = params.dataIndex;
            let date = data[dataIndex][0];
            let value = data[dataIndex][1];
            return `日期：${date}<br>字数：${value}`;
        },
        data: ["Label 1", "Label 2"],
    },
    visualMap: {
        type: "piecewise",
        splitNumber: 6,
        orient: "horizontal",
        left: "center",
        top: 0,
        textStyle: {
            color: "black",
        },
        pieces: [
            { gte: 0, lte: 0},
            { gt: 0, lte: 1000 },
            { gt: 1000, lte: 2000 },
            { gt: 2000, lte: 3000 },
            { gt: 3000, lte: 5000 },
            { gt: 5000 },
        ],
        color: [
            "#063b07",
            "#145716",
			"#2f8232",
            "#58b05b",
            "#8ccf8f",
            "#c0ebc2",
        ],
        calculable: true,
    },
    calendar: {
        left: 30,
        right: 10,
        range: currentYear,
        itemStyle: {
            normal: {
                color: "rgba(0, 0, 0, 0)",
                borderWidth: 1,
            },
        },
    },
    series: [
        {
            type: "heatmap",
            coordinateSystem: "calendar",
            data: data,
        },
    ],
};

app.plugins.plugins["obsidian-echarts"].render(option, this.container);
```
```dataviewjs
let ftMd = dv.pages("").file.sort(t => t.cday)[0]
let total = parseInt([new Date() - ftMd.ctime] / (60*60*24*1000))
let totalDays = " 您已使用 *Obsidian* "+total+" 天，"
let nofold = '!"misc/templates"'
let allFile = dv.pages(nofold).file
let totalMd = "共创建 "+
	allFile.length+" 篇笔记"
let totalTag = allFile.etags.distinct().length+" 个标签"

dv.paragraph(
	totalDays+totalMd+"、"+totalTag+""
)
```
```dataview
table without id "库中共有" +length(rows) + "个页面，总计约" + round(sum(rows.file.size)/10000,0) + "万字节（" + round((sum(rows.file.size)/1048576), 2) + "MB）" as "笔记库统计"
group by 12345
```
