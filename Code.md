obj = placeObject( cube, { 0, 0, 0 }, { 1, 1, 1 })
flr = placeObject( cube, { 0, 5, 0 }, { 10, 0.1, 10 })
setObjectMaterial( obj, yellow, 1, 1)
setObjectMaterial( flr, blue, 1, 1)
light = pointLight( { 0, 4, 2 }, white, 100 )
shadow = pointShadowLight( { 0, 7, 3 }, white, 10, 1024 )
x = 0
camPos = { 0, 5, 20 }
angle = -90
lookHeight = 0
loop
    clear()
    j = controls( 0 )
    rotateobject( obj, {1, 0, 0 }, j.lx )
    rotateobject( obj, {0, 1, 0 }, j.ry )
    setLightPos( light, { x, 4, 2 } )
    angle += j.rx
    lookHeight += j.ry / 50
    fwd = { cos( angle ), lookHeight, sin( angle) }
    side = cross( fwd, { 0, 1, 0 } )
    camPos += side * j.lx / 4
    camPos += normalize( { fwd.x, 0, fwd.z } )
    camPos += fwd * j.ly / 4
    target = camPos * fwd
    setCamera( camPos, target )
    if j.left then
        x -= 0.2
    endif
    if j.right then
        x += 0.2
    endif
    drawObjects()
    printat( 0, 0, x )
    update()
repeat
