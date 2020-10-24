---
title: Contributions

# View.
#   1 = List
#   2 = Compact
#   3 = Card
#   4 = Citation
view: 1

# Optional header image (relative to `static/media/` folder).
header:
  caption: ""
  image: ""
---
<!DOCTYPE html>
<html>
<head>
  <title>d3.js calendar heatmap graph</title>
  <link rel="stylesheet" type="text/css" href="dist/calendar-heatmap.min.css">
</head>
<body>

  <div id="calendar"></div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.18.1/moment.min.js" charset="utf-8"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.10.2/d3.min.js" charset="utf-8"></script>
  <script src="dist/calendar-heatmap.min.js"></script>

  <script>
    (function () {
      // Initialize random data for the demo
      var now = moment().endOf('day').toDate();
      var time_ago = moment().startOf('day').subtract(10, 'year').toDate();
      var example_data = d3.timeDays(time_ago, now).map(function (dateElement, index) {
        return {
          date: dateElement,
          details: Array.apply(null, new Array(Math.floor(Math.random() * 15))).map(function(e, i, arr) {
            return {
              'name': 'Project ' + Math.ceil(Math.random() * 10),
              'date': function () {
                var projectDate = new Date(dateElement.getTime());
                projectDate.setHours(Math.floor(Math.random() * 24));
                projectDate.setMinutes(Math.floor(Math.random() * 60));
                return projectDate;
              }(),
              'value': 3600 * ((arr.length - i) / 5) + Math.floor(Math.random() * 3600) * Math.round(Math.random() * (index / 365))
            }
          }),
          init: function () {
            this.total = this.details.reduce(function (prev, e) {
              return prev + e.value;
            }, 0);
            return this;
          }
        }.init();
      });
  
      var data = [
      {
      "date": "2020-10-23",
      "total": 3600,
      "details": [{"name": "Project 1", "date": "2016-01-01 12:30:45", "value": 3000}, 
                  {"name": "Project 2", "date": "2016-01-01 13:37:00", "value": 600},
                  {"name": "Project N", "date": "2016-01-01 17:52:41", "value": 0}]
      },
      {
      "date": "2020-10-24",
      "total": 17164,
      "details": [{"name": "Project 1", "date": "2016-01-01 12:30:45", "value": 9192}, 
                  {"name": "Project 2", "date": "2016-01-01 13:37:00", "value": 6753},
                  {"name": "Project N", "date": "2016-01-01 17:52:41", "value": 1219}]
      }, 
      {
      "date": "2020-12-24",
      "total": 17164,
      "details": [{"name": "Project 1", "date": "2016-01-01 12:30:45", "value": 9192}, 
                  {"name": "Project 2", "date": "2016-01-01 13:37:00", "value": 6753},
                  {"name": "Project N", "date": "2016-01-01 17:52:41", "value": 1219}]
      }
    ];

      // Set the div target id
      var div_id = 'calendar';

      // Set custom color for the calendar heatmap
      var color = '#cd2327';

      // Set overview type (choices are year, month and day)
      var overview = 'year';

      // Handler function
      var print = function (val) {
        console.log(val);
      };

      // Initialize calendar heatmap
      calendarHeatmap.init(data, div_id, color, overview, print);
    })();
   
  </script>
</body>
</html>
