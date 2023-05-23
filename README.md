# myfirst
Bar timeline charts


 <div class="row">
            <div class="col-md-4">
                <div class="">
                    <canvas id="myChart" style="width: 100%; height: 300px"></canvas>
                </div>
            </div>
  </div>

var myData = [
    { date: "01.2.2023", stage: "cutting1", PlanQty: 20, ActualQty: 10, ReqQty: 20 },
    { date: "02.2.2023", stage: "cutting2", PlanQty: 40, ActualQty: 20, ReqQty: 5 },
    { date: "03.2.2023", stage: "cutting3", PlanQty: 60, ActualQty: 50, ReqQty: 80 },
    { date: "04.2.2023", stage: "cutting4", PlanQty: 20, ActualQty: 30, ReqQty: 30 },
    { date: "05.2.2023", stage: "cutting5", PlanQty: 40, ActualQty: 50, ReqQty: 60 },
    { date: "06.2.2023", stage: "cutting6", PlanQty: 30, ActualQty: 70, ReqQty: 70 },
    { date: "07.2.2023", stage: "cutting7", PlanQty: 70, ActualQty: 60, ReqQty: 30 },
    { date: "08.2.2023", stage: "cutting8", PlanQty: 90, ActualQty: 20, ReqQty: 50 },
    { date: "09.2.2023", stage: "cutting9", PlanQty: 0, ActualQty: 0, ReqQty: 20 }
];

function drawChart() {
    var labels = [];
    var startDate = [];
    var endDate = [];

    for (var i = 0; i < myData.length; i++) {
        labels.push(myData[i].stage);
        startDate.push(myData[i].date);
        // Calculate the end date based on the start date and the duration of each stage
        var duration = i === myData.length - 1 ? 0 : 1; // Assuming each stage has a duration of 1 day
        var endDateValue = new Date(myData[i].date);
        endDateValue.setDate(endDateValue.getDate() + duration);
        endDate.push(endDateValue.toISOString().split("T")[0]);
    }

    var ctx = document.getElementById('myChart').getContext('2d');
    new Chart(ctx, {
        type: 'horizontalBar',
        data: {
            labels: labels,
            datasets: [{
                label: 'Timeline',
                data: startDate.map((start, index) => {
                    return {
                        x: start,
                        y: labels[index],
                        x2: endDate[index]
                    };
                }),
                backgroundColor: '#b33dc6',
            }]
        },
        options: {
            plugins: {
                title: {
                    display: true,
                    text: 'Timeline Chart',
                    font: {
                        size: 12
                    }
                }
            },
            scales: {
                x: {
                    type: 'time',
                    time: {
                        unit: 'day',
                        tooltipFormat: 'DD.MM.YYYY' // Adjust the tooltip format as per your preference
                    },
                    display: true,
                    offset: true
                },
                y: {
                    display: true
                }
            },
            responsive: true,
            maintainAspectRatio: false
        }
    });
}
