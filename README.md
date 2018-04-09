python QR Code generator
=============================

Generate QR codes.

For a standard install (which will include pillow_ for generating images),
run::

    pip install qrcode[pil]

.. _pillow: https://pypi.python.org/pypi/Pillow

Usage
=====

From the command line, use the installed ``qr`` script::

    qr "Some text" > test.png

Or in Python, use the ``make`` shortcut function:

.. code:: python

    import qrcode
    img = qrcode.make('Some data here')

Advanced Usage
--------------

For more control, use the ``QRCode`` class. For example:

.. code:: python

    import qrcode
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_L,
        box_size=10,
        border=4,
    )
    qr.add_data('Some data')
    qr.make(fit=True)

    img = qr.make_image(fill_color="black", back_color="white")

From your command line::

    qr --factory=svg-path "Some text" > test.svg
    qr --factory=svg "Some text" > test.svg
    qr --factory=svg-fragment "Some text" > test.svg

Or in Python:

.. code:: python

    import qrcode
    import qrcode.image.svg

    if method == 'basic':
        # Simple factory, just a set of rects.
        factory = qrcode.image.svg.SvgImage
    elif method == 'fragment':
        # Fragment factory (also just a set of rects)
        factory = qrcode.image.svg.SvgFragmentImage
    else:
        # Combined path factory, fixes white space that may occur when zooming
        factory = qrcode.image.svg.SvgPathImage

    img = qrcode.make('Some data here', image_factory=factory)

Two other related factories are available that work the same, but also fill the
background of the SVG with white::

    qrcode.image.svg.SvgFillImage
    qrcode.image.svg.SvgPathFillImage

From your command line::

    qr --factory=pymaging "Some text" > test.png

Or in Python:

.. code:: python

    import qrcode
    from qrcode.image.pure import PymagingImage
    img = qrcode.make('Some data here', image_factory=PymagingImage)
