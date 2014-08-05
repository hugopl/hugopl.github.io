---
layout: post
title:  "It's benchmark time!"
tags: meique cmake
---
I started to write my [own build system](/2009/12/05/Reinventing-the-wheel-to-save-the-universe.html) for C++ years ago, at my own pace, one line at the time... and sometimes no lines at all. Last months I did work a bit more on it and nowadays I would consider it in a pretty good shape, so it's time for a benchmark!

The motivations behind of benchmarking [meique](http://www.meique.org) (BTW this is the project name) was the most pure act of human curiosity, mainly after read about the [tup benchmak](http://gittup.org/tup/make_vs_tup.html).

Meique is slower than tup, on the other hand it doesn't need the "complicated" tup setup, run with suid, etc. So my comparison here is with 2 other contenders: CMake/make and CMake/ninja.

## Metodology

The metodology is very similar to the one used by the tup benchmak, just the code generator differ, so there's a dummy C project with 4 shared libraries, and a main.c that uses them all, the number of files per shared libraries increase in each round, first 10 then 100, 1000 and 10000. i.e. 41, 401, 4001 and a 40001 files project. On each round the following operations are done:

* Clean build.
* Touch a header, then trigger a build.
* Touch a .c file, then trigger a build.
* Do nothing, then trigger a build.

Except for clean build, all other operations are repeated 3 times and the mean is used as result, there are also some other details that you can check in the [run-test.sh](https://github.com/Meique/Meique/tree/master/benchmark) script.

The computer used was a 8 cores intel i7 machine with 16GB on a hardware enabled RAID 0, make was ran with -j9.

## Results

For my surprise, meique is faster than CMake/make and as expected it's slower than CMake/ninja. Since speed is a concern but not the meique main focus as it's on ninja I consider the results very good.

Ninja isn't showing in the results due to a bug, it can't link a shared library with 10000 files due to the very long argument list, meique had this very same bug, now fixed.

<script type="text/javascript" src="/highcharts.js"></script>
<script type="text/javascript">
$(function () {
$('#initial').highcharts({
    chart: {
        type: 'spline',
    },
    title: {
        text: 'initial'
    },
    subtitle: {
        text: '5 modules depending on a single module'
    },
    xAxis: {
        type: 'logarithmic',
        title: {
            enabled: true,
            text: 'Number of files per module'
        },
        labels: {
            formatter: function() {
                return this.value;
            }
        },
    },
    yAxis: {
        type: 'logarithmic',
        title: {
            text: 'seconds'
        },
    },
    legend: {
        enabled: true
    },
    tooltip: {
        headerFormat: '<b>{series.name}</b><br/>',
        pointFormat: '{point.x} file per module,<br />{point.y} seconds'
    },
    series: [{
        name: "cmake/make",
        data: [[10, 1.34], [100, 3.1], [1000, 23.75], [10000, 304.15], ]
        },{
        name: "meique",
        data: [[10, 0.34], [100, 1.72], [1000, 15.45], [10000, 155.91], ]
        },]
    });
$('#0c_touched').highcharts({
    chart: {
        type: 'spline',
    },
    title: {
        text: '0.c touched'
    },
    subtitle: {
        text: '5 modules depending on a single module'
    },
    xAxis: {
        type: 'logarithmic',
        title: {
            enabled: true,
            text: 'Number of files per module'
        },
        labels: {
            formatter: function() {
                return this.value;
            }
        },
    },
    yAxis: {
        type: 'logarithmic',
        title: {
            text: 'seconds'
        },
    },
    legend: {
        enabled: true
    },
    tooltip: {
        headerFormat: '<b>{series.name}</b><br/>',
        pointFormat: '{point.x} file per module,<br />{point.y} seconds'
    },
    series: [{
        name: "cmake/make",
        data: [[10, 0.20000000000000004], [100, 0.24], [1000, 0.6866666666666666], [10000, 10.266666666666666], ]
        },{
        name: "meique",
        data: [[10, 0.16], [100, 0.19666666666666668], [1000, 0.5466666666666667], [10000, 6.446666666666666], ]
        },]
    });
$('#0h_touched').highcharts({
    chart: {
        type: 'spline',
    },
    title: {
        text: '0.h touched'
    },
    subtitle: {
        text: '5 modules depending on a single module'
    },
    xAxis: {
        type: 'logarithmic',
        title: {
            enabled: true,
            text: 'Number of files per module'
        },
        labels: {
            formatter: function() {
                return this.value;
            }
        },
    },
    yAxis: {
        type: 'logarithmic',
        title: {
            text: 'seconds'
        },
    },
    legend: {
        enabled: true
    },
    tooltip: {
        headerFormat: '<b>{series.name}</b><br/>',
        pointFormat: '{point.x} file per module,<br />{point.y} seconds'
    },
    series: [{
        name: "cmake/make",
        data: [[10, 0.25333333333333335], [100, 0.2866666666666667], [1000, 0.6533333333333333], [10000, 9.946666666666665], ]
        },{
        name: "meique",
        data: [[10, 0.17666666666666667], [100, 0.21333333333333335], [1000, 0.53], [10000, 6.36], ]
        },]
    });
$('#nothing').highcharts({
    chart: {
        type: 'spline',
    },
    title: {
        text: 'nothing'
    },
    subtitle: {
        text: '5 modules depending on a single module'
    },
    xAxis: {
        type: 'logarithmic',
        title: {
            enabled: true,
            text: 'Number of files per module'
        },
        labels: {
            formatter: function() {
                return this.value;
            }
        },
    },
    yAxis: {
        type: 'logarithmic',
        title: {
            text: 'seconds'
        },
    },
    legend: {
        enabled: true
    },
    tooltip: {
        headerFormat: '<b>{series.name}</b><br/>',
        pointFormat: '{point.x} file per module,<br />{point.y} seconds'
    },
    series: [{
        name: "cmake/make",
        data: [[10, 0.08666666666666667], [100, 0.11333333333333333], [1000, 0.3666666666666667], [10000, 8.456666666666667], ]
        },{
        name: "meique",
        data: [[10, 0.01], [100, 0.03666666666666667], [1000, 0.26], [10000, 4.75], ]
        },]
    });
});
</script>
<div id="initial"></div>

1.95x faster on the 40K files project! And I don't know why because clean build is the most simple task.

<div id="0c_touched"></div><br>
<div id="0h_touched"></div><br>
<div id="nothing"></div>

There are still much room for improvements on meique, so the next goal is simple: to be faster than a ninja! ;-)
