# libdwgx
OpenSource library under X11/MIT license for everyday use. Under development, but some of basic functionality is already available.

All help will be very good for project. A lot of TODO's in code, so you can fix something you want.

API
---
libdwgx typical usage pipeline is shown below:
Open .DWG file:
```cpp
DWGFile * opendwg = libdwgx::InitializeDWG("/path/to/example.dwg");

opendwg->ReadHeader();
opendwg->ReadObjectMap();
```

From now on, you can access geometries like this:
```cpp
int geometries_count = opendwg->GetGeometriesCount();
for(auto i = 0; i < geometries_count; ++i)
{
    libdwgx::DWGGeometries::Geometry * geom = dwgfile->ReadGeometry (i);
    // now, geom->sGeometryType stores a type of returned geometry. Then,
    // you have to cast it to this class, eg.
    if ( geom->sGeometryType == libdwgx::DWGGeometries::DWGGeometryType::CIRCLE )
    {
        libdwgx::DWGGeometries::Circle * circle = geom;
        // There you go. Now you can get all the data you want, eg.
        std::cout << circle->dfCenterX;
        std::cout << circle->dfCenterY;
        std::cout << circle->dfCenterZ;
        std::cout << circle->dfRadius;
    }
}
```

Now supported DWG version are:

1. R2000 (read-only). Its under development still, and a lot of geometries are missed, but it will all come with time.
2. Next up on the list: R2004.

Build status
------------
Linux: [![Build Status](https://travis-ci.org/sandyre/libdwgx.svg?branch=master)](https://travis-ci.org/sandyre/libdwgx)
