IMF
===

Simple tools to work with the Initial Mass Function

.. image:: examples/plots/imf.png

Some basic examples below.

 1. Make a simple 1000 Msun cluster sampled from the default Kroupa IMF::

     cluster = imf.make_cluster(1000)

    or from a Salpeter IMF::

     cluster = imf.make_cluster(1000, massfunc='salpeter')

 1. Create a sample of clusters to do some analysis of later.  This will make clusters
    with masses Gaussian-distributed around a given mean mass in the list of
    cluster_masses, so that you could then do things like estimate the typical
    luminosity of a cluster for a given mass::

    from imf import imf
    from astropy.utils.console import ProgressBar
    cluster_masses = [100, 1000, 10000]
    nclusters_per_bin = 30
    clusters = np.array([[imf.make_cluster(mass*(np.random.randn()/20.+1.), silent=True)
                          for ii in range(nclusters_per_bin)]
                          for mass in ProgressBar(cluster_masses)])

 1. Calculate the mass fraction represented by M>8 Msun stars in a Kroupa IMF when
    the maximum mass is 200 Msun::


      kroupa = imf.Kroupa()

      mmax = 200
      cutoff1 = 8

      over8fraction = (kroupa.m_integrate(cutoff1, mmax)[0] /
                       kroupa.m_integrate(kroupa.mmin, mmax)[0])


.. image:: https://d2weczhvl823v0.cloudfront.net/keflavich/imf/trend.png
   :alt: Bitdeli badge
   :target: https://bitdeli.com/free

