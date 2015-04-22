---
title: Graphical Representation of my model data ie charts in ruby on rails using highcharts
author: Mohit Jain
layout: post
comments: true



permalink: /2013/02/graphical-representation-of-my-model-data-charts-in-ruby-on-rails-using-highcharts/
categories: General ruby-on-rails
---

We all need to see whats going on with my website. Is it running smooth, Whats the status of the users signup etc.

Take a look on these two graphs ([Live demo][1]).

 [1]: http://highchartsgraphs.herokuapp.com/ "Highcharts in ruby on rails"

1. Graphs for total records (users, activities) on each day in the range of last 30 days.

![Total Records Growth](/wp-content/uploads/2013/02/Total-Growth.png?fit=750,274)

2. Graphs for total daily records (users signed up that day, activities done that day) in the range of last 30 days.

![Total Daily Based](/wp-content/uploads/2013/02/Total-Daily-Based.png?fit=750,274)


So for building these graphs, which are pretty useful, there are just few steps

* Include Jquery [Highcharts Libray.][6]
* Include rails module in your lib file.
* Include module in specific models for which you need to show graphs.
* Paste some js code and you are done.

 [6]: http://www.highcharts.com/ "Highcharts librayr"

<!--more-->

## Step 1

Include jquery library and exporting.js and highcharts.js files which you can easily find [here][7]

 [7]: http://www.highcharts.com/download "Download Highcharts"

##Step 2

Include act\_as\_coutable.rb in your lib directory and specify these in your application.rb file.

{% highlight ruby %}

#lib/modules/act_as_coutable.rb
module ActAsCountable
  def self.included(base)
    base.extend(ClassMethods)
  end

  module ClassMethods
    def total_records_counts_array_in_past_n_days(range = 30.days)
      total_records = []
      counts =  self.group('Date(created_at)').count
      (30.days.ago.to_date..Date.today).each do |day|
        total_records.push((total_records.last || )  (counts[day] || ))
      end
      total_records
    end

    def daily_records_counts_array_in_past_n_days(range = 30.days)
      counts = self.group('Date(created_at)').count
      (range.ago.to_date..Date.today).map {|date| counts[date] || }
    end
  end
end

{% endhighlight %}

Auto load this module

{% highlight ruby %}

/config/application.rb
config.autoload_paths  = %W(#{config.root}/lib)
config.autoload_paths  = Dir["#{config.root}/lib/**/"]
config.autoload_paths  = Dir["#{config.root}/lib/modules/**"]
{% endhighlight %}

In models, include the module

{% highlight ruby %}

class User < ActiveRecord::Base
  include ActAsCountable
  # other methods etc.
end

class Activity < ActiveRecord::Base
  include ActAsCountable
  # other methods etc.
end

{% endhighlight %}

So now all we need is the view file and here is the code for the same:

##For Daily Growth Chart ie first one:

{% highlight javascript %}

$(function () {
	var chart;
	$(document).ready(function() {
		chart = new Highcharts.Chart({
			chart: {
				renderTo: 'daily_growth'
			},
			title: {
				text: 'Incremental Growth Charts - Gifts'
			},
			xAxis: {
				type: 'datetime'
			},
			yAxis: {
				title: {
					text: 'Counts'
				}
			},
			tooltip: {
				formatter: function() {
					return ''
					Highcharts.dateFormat('%e. %b', this.x)  ' -> '  this.y;
				}
			},
			plotOptions: {
				spline: {
					lineWidth: 4,
					states: {
						hover: {
							lineWidth: 5
						}
					},
					marker: {
						enabled: false,
						states: {
							hover: {
								enabled: true,
								symbol: 'circle',
								radius: 5,
								lineWidth: 1
							}
						}
					}
				}
			},
			series: [
			{
				name: 'Total Signups Today',
				pointInterval: ,
				pointStart: ,
				data:

			}, {
				name: 'Total Activities Tday',
				pointInterval: ,
				pointStart: ,
				data:
			}

			]
			,
			navigation: {
				menuItemStyle: {
					fontSize: '10px'
				}
			}
		});
	});

});

{% endhighlight %}


##For Total Records Chart ie second one:



{% highlight javascript %}

$(function () {
	var chart;
	$(document).ready(function() {
		chart = new Highcharts.Chart({
			chart: {
				renderTo: 'growth_rate'
			},
			title: {
				text: 'Growth Charts - Users and User Activities'
			},
			xAxis: {
				type: 'datetime'
			},
			yAxis: {
				title: {
					text: 'Counts'
				}
			},
			tooltip: {
				formatter: function() {
					return ''
					Highcharts.dateFormat('%e. %b', this.x)  ' -> '  this.y;
				}
			},
			plotOptions: {
				spline: {
					lineWidth: 4,
					states: {
						hover: {
							lineWidth: 5
						}
					},
					marker: {
						enabled: false,
						states: {
							hover: {
								enabled: true,
								symbol: 'circle',
								radius: 5,
								lineWidth: 1
							}
						}
					}
				}
			},
			series: [
			{
				name: 'Total Signups Today',
				pointInterval: ,
				pointStart: ,
				data:

			}, {
				name: 'Total Activities Tday',
				pointInterval: ,
				pointStart: ,
				data:
			}
			]
			,
			navigation: {
				menuItemStyle: {
					fontSize: '10px'
				}
			}
		});
	});

});

{% endhighlight %}



One more last thing. If you want to see stat counters on graph itself ie:

Change the plot options in javascript code to this:
![Graphs for admin panel](/wp-content/uploads/2013/02/chart.png?fit=800,274)

{% highlight javascript %}

plotOptions: {
	line: {
		dataLabels: {
			enabled: true
		},
		enableMouseTracking: false
	}
},

{% endhighlight %}
