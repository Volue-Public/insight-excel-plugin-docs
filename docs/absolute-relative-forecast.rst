.. _absolute-relative-forecast:

Absolute and Relative Forecast
==============================

This section describes about how to generate of absolute and relative forecast data with Volue Insight API add-in on excel:

*********************
Absolute Forecast
*********************

#. First, select the cell on the right side of the Absolute cell. 

    .. image:: /_static/images/excel-plugin-absolute-navigation.png
       :width: 200

#. The absolute forecast options would appear on the right (add-in).

    .. image:: /_static/images/excel-plugin-absolute-page.png
        :width: 250

#. The first and second option are the Issue Date From and Issue Date To respectively. These allow user to pick the issue date from and to, meanwhile the default issue date is the latest. 

    .. image:: /_static/images/excel-plugin-absolute-issue-dates.png
            :width: 250

#. The next option is the Date Time. The user can filter the date and time of the forecast date. 

    .. image:: /_static/images/excel-plugin-absolute-date-time.png
            :width: 250

#. The last option is the issue frequency options, which is frequency for the output time series. Thus, user could also choose the issue frequency. 

    .. image:: /_static/images/excel-plugin-issue-frequency.png
            :width: 250

#. After giving the input, click Submit button.

    .. image:: /_static/images/excel-plugin-absolute-submit.png
            :width: 250

#. Then, the parameter is being added on the cell.

    .. image:: /_static/images/excel-plugin-absolute-parameter.png
            :width: 600

#. Furthermore, you can also edit the parameters directly on the cell, or using the Clear button to remove all.

#. Finally, click the refresh or refresh all button on navigation to get the data out.

     .. image:: /_static/images/excel-plugin-absolute-refresh.png
            :width: 250

You can find out more about absolute forecast Volue Insight API on:  https://volueinsight.com/docs/api/api-absolute-relative-forecast.html

*********************
Relative Forecast
*********************

#. To navigate the relative forecast, select the cell on the right of the Relative cell

    .. image:: /_static/images/excel-plugin-relative-navigate.png
                :width: 250

#. Then the relative forecast options would appear on right (add-in).

    .. image:: /_static/images/excel-plugin-relative-page.png
                :width: 250

#. The input form has similiarity with Absolute Forecast, such as Issue Dates picker.

    .. image:: /_static/images/excel-plugin-relative-issue-dates.png
                :width: 250

#. There are difference features, such as the Offset and Max Length. The Offset allows user to define the data offset from the starting of issue date. Meanwhile, the Max length is to define when the subset end. 

     .. image:: /_static/images/excel-plugin-relative-offsets-max.png
                :width: 250

#. Another feature is Filter for Issue Dates, given the options of different types of time periods. 

    .. image:: /_static/images/excel-plugin-relative-filter-issue-dates.png
                    :width: 250       
    .. image:: /_static/images/excel-plugin-relative-filter-issue-dates-options.png
                    :width: 250
                
#. After giving the input, click Submit button.

    .. image:: /_static/images/excel-plugin-relative-submit.png
                :width: 250

#. Then, the parameter is being added on the cell.

    .. image:: /_static/images/excel-plugin-relative-parameter.png
                :width: 600

#. Furthermore, we can also edit directly on the cell, or using the Clear button to remove all.

#. Finally, click the refresh or refresh all button on navigation to get the data out.

    .. image:: /_static/images/excel-plugin-absolute-refresh.png
            :width: 250


.. warning::
    The Absolute and Relative forecast can not work at the same time together. Moreover, the issue dates work independently for its feature, thus it is not the same as the Issue Date on the curve table.  


You can find out more about relative forecast Volue Insight API on:  https://volueinsight.com/docs/api/api-absolute-relative-forecast.html

