A rather incomplete Cython wrapper for https://code.google.com/p/polypartition/

you can chuck a list of tuples representing a polygon at it and get a list of triangles and convex hulls
order must be counter-clockwise for non-holes, clockwise for holes.

build with

    python2 setup.py build_ext --inplace

example:

    import pypolypart
    poly1 = [(0,0),(10,0), (9,5), (10,10),(0,10)]
    poly2 = [(99+0,0),(99+10,0), (99+9,5), (99+10,10),(99+0,10)]
    hole1 = [(1,1),(1,3), (3,1)]
    print pypolypart.polys_to_tris_and_hulls([poly1, poly2], [hole1])

output:

    {
     'hulls':[
       [(99.0, 0.0), (109.0, 0.0), (108.0, 5.0), (99.0, 10.0)],
       [(99.0, 10.0), (108.0, 5.0), (109.0, 10.0)],
       [(0.0, 0.0), (10.0, 0.0), (3.0, 1.0), (1.0, 1.0)], 
       [(0.0, 10.0), (0.0, 0.0), (1.0, 1.0), (1.0, 3.0)], 
       [(1.0, 3.0), (3.0, 1.0), (10.0, 0.0), (9.0, 5.0), (0.0, 10.0)], [(9.0, 5.0), (10.0, 10.0), (0.0, 10.0)]
       ],
     'triangles': [
      [(99.0, 0.0), (109.0, 0.0), (108.0, 5.0)], 
      [(99.0, 10.0), (99.0, 0.0), (108.0, 5.0)], 
      [(99.0, 10.0), (108.0, 5.0), (109.0, 10.0)], 
      [(0.0, 0.0), (10.0, 0.0), (3.0, 1.0)], 
      [(0.0, 0.0), (3.0, 1.0), (1.0, 1.0)], 
      [(0.0, 10.0), (0.0, 0.0), (1.0, 1.0)], 
      [(0.0, 10.0), (1.0, 1.0), (1.0, 3.0)], 
      [(3.0, 1.0), (10.0, 0.0), (9.0, 5.0)], 
      [(9.0, 5.0), (10.0, 10.0), (0.0, 10.0)], 
      [(9.0, 5.0), (0.0, 10.0), (1.0, 3.0)], 
      [(9.0, 5.0), (1.0, 3.0), (3.0, 1.0)]
     ]
    }

Troubleshooting:

Try drawing your polygon - is it a normal polygon? do any parts self-intersect? are there any doubled points? infinitly thin areas?  
Check is it winding in the correct direction? Try simplifying it by removing points too close to other points (see pygametest for a simple function for this).  
Finally - try sub-sections of your polygon, see if you can discover the "Problem Area"
    
keywords: optimal convex hull decomposition partition generation split segment physics triangulation Hertel-Mehlhorn
ear clipping Keil-Snoeyink monotone
