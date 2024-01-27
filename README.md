# utl-AI-computer-vision-fitting-a-circle-to-a-scatter-plot-of-points-wps-r
AI computer vision fitting a circle to a scatter plot of points 
    %let pgm=utl-AI-computer-vision-fitting-a-circle-to-a-scatter-plot-of-points-wps-r;

    AI computer vision fitting a circle to a scatter plot of points

    github
    http://tinyurl.com/bdhkchck
    https://github.com/rogerjdeangelis/utl-AI-computer-vision-fitting-a-circle-to-a-scatter-plot-of-points-wps-r

    Very simple example of fitting a circle or elipsoid to messy scatter plot.
    Consider it the outline of a head, can use pixels.

    see this pacakge can (do much more than fit  circle - elipse fits);
    Good to estimate the contours os a head.
    https://cran.r-project.org/web/packages/conicfit/conicfit.pdf

    Other AI Repos
    https://github.com/rogerjdeangelis/utl-AI-compute-the-distance-between-objects-in-an-image-python
    https://github.com/rogerjdeangelis/utl-AI-first-name-and-birth-date-range-to-gender
    https://github.com/rogerjdeangelis/utl-AI-geometry-is-the-figure-a-right-triangle-
    https://github.com/rogerjdeangelis/utl-AI-internal-angles-of-polygon-from-vertex-coordinates-in-r
    https://github.com/rogerjdeangelis/utl-AI-labeling-centroids-inside-and-within-a-boundary-polygon
    https://github.com/rogerjdeangelis/utl-AI-remove-noise-from-an-image-python-opencv
    https://github.com/rogerjdeangelis/utl-AI-spelling-corrector-when-word-is-close-to-the-correct-word
    https://github.com/rogerjdeangelis/utl-R-AI-igraph-list-connections-in-a-non-directed-graph-for-a-subset-of-vertices

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                       INPUT                                                                                            */
    /*                                                        PROCESS                           OUTPUT                        */
    /*                                                                                                                        */
    /*      -200     -100       0       100      200                                -200     -100       0       100      200  */
    /*      --+--------+--------+--------+--------+--   want <-                     --+--------+--------+--------+--------+-- */
    /*   Y |                                        |    CircleFitByLandau(xy);    |                                        | */
    /*     |                                        |                              |      RADIUS     X-ORIGIN    Y-ORIGIN   | */
    /*     |                                        |                              | sqrt(203.038**2-(X-1.711)**2) + 0      | */
    /*     |         *         |   * *  *           |       RADIUS   = 203.038     |                                        | */
    /*     |          **    ** | *       *          |       X_ORIGIN = -1.711      |                                        | */
    /* 200 +   *  **          ** **   *             + 200   Y_ORIGIN = 0.000     200 +            ++++++++++++++            + */
    /*     |     *      *** *  |    *  ***       *  |                              |         +++       |       ++           | */
    /*     |       *     *   * |    *   **   *      |                              |       ++          |         ++         | */
    /*     |        ** *  *    | *  **              |                              |     ++            |            ++      | */
    /*     |    ** *  **     * | *    *     ** **   |                              |    ++             |             ++     | */
    /* 100 +   *  * *          |          *   *     + 100                      100 +   ++              |               +    + */
    /*     |   *               |                    |                              |  ++               |                +   | */
    /*     | **                |                 *  |                              |  +                |                    | */
    /*     |                   |            * *     |                              | +                 |                 +  | */
    /*     |                   |                *   |                              |                   |                 +  | */
    /*   0 +-------------------+------------------- + 0                          0 +-------------------+------------------- + */
    /*     |                   |                *   |                              |                   |                 +  | */
    /*     |                   |            * *     |                              | +                 |                 +  | */
    /*     | **                |                 *  |                              |  +                |                    | */
    /*     |   *               |                    |                              |                   |                +   | */
    /* 100 +   *  * *          |          *   *     + 100                      100 +   +               |               +    + */
    /*     |    ** *  **     * | *    *     ** **   |                              |    +              |             ++     | */
    /*     |        ** *  *    | *  **              |                              |     ++            |            ++      | */
    /*     |       *     *   * |    *   **   *      |                              |       ++          |         ++         | */
    /*     |     *      *** *  |    *  ***       *  |                              |         ++++      |     ++++           | */
    /* 200 +   *  **          ** **   *             + 200                      200 +            ++++++++++++++              + */
    /*     |          **    ** | *       *          |                              |                   |                    | */
    /*       --+--------+--------+--------+--------+-                               --+--------+--------+--------+--------+-- */
    /*      -200     -100      0         100      200                               -200     -100       0       100      200  */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  SD1.HAVE total obs=158                                                                                                */
    /*                                                                                                                        */
    /*  Obs        x           y                                                                                              */
    /*                                                                                                                        */
    /*    1    -199.802      59.505                                                                                           */
    /*    2    -199.802     -59.505                                                                                           */
    /*    3    -193.496      68.193                                                                                           */
    /*    4    -193.496     -68.193                                                                                           */
    /*    5    -182.174      81.413                                                                                           */
    /*                                                                                                                        */
    /*  153     199.390      66.369                                                                                           */
    /*  154     199.390     -66.369                                                                                           */
    /*  155     175.020     113.711                                                                                           */
    /*  156     175.020    -113.711                                                                                           */
    /*  157     196.251     188.399                                                                                           */
    /*  158     196.251    -188.399                                                                                           */
    /*                                                                                                                        */
    /***********************************************************************************************************************  */

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    proc datasets lib=sd1 nolist mt=data mt=view nodetails;delete have; run;quit;

    %utl_submit_wps64x('

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have(keep=x y);
     call streaminit(1);
     do xs= -200 to 200 by 5;
       x=xs + rand("normal",0,10);
       y=sqrt(40000 - x**2) + rand("normal",0,50);
       if y ne . then do;
          output;
          y=-y;
          output;
       end;
     end;
    run;quit;

    options ls=64 ps=54;
    proc plot data=sd1.have;
      plot y*x="*"/
        href=0 vref=0 haxis=-200 to 200 by 100 vaxis=-200 to 200 by 100;
    run;quit;
    ');

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* SD1.HAVE total obs=158                                                                                                 */
    /*                                                                                                                        */
    /* Obs        x           y                                                                                               */
    /*                                                                                                                        */
    /*   1    -199.802      59.505                                                                                            */
    /*   2    -199.802     -59.505                                                                                            */
    /*   3    -193.496      68.193                                                                                            */
    /*   4    -193.496     -68.193                                                                                            */
    /*   5    -182.174      81.413                                                                                            */
    /*                                                                                                                        */
    /* 153     199.390      66.369                                                                                            */
    /* 154     199.390     -66.369                                                                                            */
    /* 155     175.020     113.711                                                                                            */
    /* 156     175.020    -113.711                                                                                            */
    /* 157     196.251     188.399                                                                                            */
    /* 158     196.251    -188.399                                                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    proc datasets lib=sd1 nolist mt=data mt=view nodetails;delete want; run;quit;

    options ls=171 ps=65;
    %utl_submit_wps64x('
    libname sd1 sas7bdat "d:/sd1";
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;
    library(conicfit);
    xy  <- as.matrix(have);
    want <- as.data.frame(CircleFitByLandau(xy));
    colnames(want)<-c("x_origin","y_origin","radius");
    endsubmit;
    import r=want data=sd1.want;
    run;quit;

    data _null_;
       set sd1.want;
       call symputx("radius",put(radius,9.3));
       call symputx("x_origin",put(x_origin,9.3));
       call symputx("y_origin",put(y_origin,9.3));
     run;quit;

    %put &=radius;
    %put &=x_origin;
    %put &=y_origin;

    %put formula = sqrt(&radius**2 - (x - (&x_origin.))**2) + &y_origin.;
    data want;
       set sd1.have;
       ycir=sqrt(&radius**2 - (x - &x_origin.)**2) + &y_origin.;
       output;
       ycir=-ycir;
       output;
    run;quit;

    options ls=64 ps=44;
    proc plot data=want;
      plot ycir*x="+" / box
     href=0 vref=0 haxis=-200 to 200 by 100 vaxis=-200 to 200 by 100;;
    run;quit;
    ');

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS PLOT Procedure                                                                                                 */
    /*                               X                                                                                        */
    /*      -200         -100           0           100          200                                                          */
    /*       -+------------+------------+------------+------------+-                                                          */
    /*  YCIR |                          |                          | YCIR                                                     */
    /*       |                          |                          |                                                          */
    /*   200 +                 +++ + +++++ ++++++                  +  200                                                     */
    /*       |              ++++        |        + +++             |                                                          */
    /*       |         ++++             |            +++           |                                                          */
    /*       |       +++                |                  +       |                                                          */
    /*       |     ++                   |                  +++     |                                                          */
    /*       |    +                     |                    +     |                                                          */
    /*   100 +  +                       |                      +   +  100                                                     */
    /*       |                          |                       +  |                                                          */
    /*       | +                        |                          |                                                          */
    /*       |+                         |                         +|                                                          */
    /*       |                          |                         +|                                                          */
    /*       |                          |                          |                                                          */
    /*     0 +--------------------------+--------------------------+  0                                                       */
    /*       |                          |                          |                                                          */
    /*       |                          |                         +|                                                          */
    /*       |+                         |                         +|                                                          */
    /*       | +                        |                          |                                                          */
    /*       |                          |                       +  |                                                          */
    /*  -100 +  +                       |                      +   + -100                                                     */
    /*       |    +                     |                    +     |                                                          */
    /*       |     ++                   |                  +++     |                                                          */
    /*       |       +++                |                  +       |                                                          */
    /*       |         ++++             |            +++           |                                                          */
    /*       |              ++++        |        + +++             |                                                          */
    /*  -200 +                 +++ + +++++ ++++++                  + -200                                                     */
    /*       -+------------+------------+------------+------------+-                                                          */
    /*      -200         -100           0           100          200                                                          */
    /*                                                                                                                        */
    /*                                  X                                                                                     */
    /*                                                                                                                        */
    /*      ciccle(x) = sqrt(203.038**2 - (x - (-1.711))**2) + 0.000                                                          */
    /*                                                                                                                        */
    /*      radius    = 203.038                                                                                               */
    /*      x_origin  = -1.711                                                                                                */
    /*      y_origin  = 0.000                                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
