GuiGraphCtrl
============

A control that plots one or more curves in a chart.

Inherit:
	:doc:`GuiControl`

Description
-----------

Up to 6 individual curves can be plotted in the graph. Each plotted curve can have its own display style including its own charting style (plotType) and color (plotColor).

The data points on each curve can be added in one of two ways:

Example::

	// Create a graph that plots a red polyline graph of the FPS counter in a 1 second (1000 milliseconds) interval.newGuiGraphCtrl( FPSGraph )
	{
	   plotType[ 0 ] = "PolyLine";
	   plotColor[ 0 ] = "1 0 0";
	   plotVariable[ 0 ] = "fps::real";
	   plotInterval[ 0 ] = 1000;
	};

Methods
-------

.. cpp:function:: void GuiGraphCtrl::addAutoPlot(int plotId, string variable, int updateFrequency)

	Sets up the given plotting curve to automatically plot the value of the variable with a frequency of updateFrequency .

	:param plotId: Index of the plotting curve. Must be 0<=plotId<6.
	:param variable: Name of the global variable.
	:param updateFrequency: Frequency with which to add new data points to the plotting curve (in milliseconds).

	Example::

		// Plot FPS counter at 1 second intervals.
		%graph.addAutoPlot( 0, "fps::real", 1000 );

.. cpp:function:: void GuiGraphCtrl::addDatum(int plotId, float value)

	Add a data point to the plot's curve.

	:param plotId: Index of the plotting curve to which to add the data point. Must be 0<=plotId<6.
	:param value: Value of the data point to add to the curve.

.. cpp:function:: float GuiGraphCtrl::getDatum(int plotId, int index)

	Get a data point on the given plotting curve.

	:param plotId: Index of the plotting curve from which to fetch the data point. Must be 0<=plotId<6.
	:param index: Index of the data point on the curve.

	:return:  are out of range. 

.. cpp:function:: void GuiGraphCtrl::matchScale(int plotID1, int plotID2,  ...)

	Set the scale of all specified plots to the maximum scale among them.

	:param plotID1: Index of plotting curve.
	:param plotID2: Index of plotting curve.

.. cpp:function:: void GuiGraphCtrl::removeAutoPlot(int plotId)

	Stop automatic variable plotting for the given curve.

	:param plotId: Index of the plotting curve. Must be 0<=plotId<6.

.. cpp:function:: void GuiGraphCtrl::setGraphType(int plotId, GuiGraphType graphType)

	Change the charting type of the given plotting curve.

	:param plotId: Index of the plotting curve. Must be 0<=plotId<6.
	:param graphType: Charting type to use for the curve.

Fields
------

.. cpp:member:: float  GuiGraphCtrl::centerY

	Ratio of where to place the center coordinate of the graph on the Y axis. 0.5=middle height of control. This allows to account for graphs that have only positive or only negative data points, for example.

.. cpp:member:: ColorF  GuiGraphCtrl::plotColor [6]

	Color to use for the plotting curves in the graph.

.. cpp:member:: int  GuiGraphCtrl::plotInterval [6]

	Interval between auto-plots of plotVariable for the respective curve (in milliseconds).

.. cpp:member:: GuiGraphType GuiGraphCtrl::plotType [6]

	Charting type of the plotting curves.

.. cpp:member:: string  GuiGraphCtrl::plotVariable [6]

	Name of the variable to automatically plot on the curves. If empty, auto-plotting is disabled for the respective curve.
