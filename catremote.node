var five = require("johnny-five")
var server = require("http").createServer()
var io = require("socket.io")(server)

var board = new five.Board()

board.on("ready", function () {
  console.log("Board ready")

  var vert = new five.Servo(13)
  var hoz = new five.Servo(10)
  var laser = new five.Led(7)

  var laserTimeout = null

  function fireLaser () {
    laser.on()
    clearTimeout(laserTimeout)
    laserTimeout = setTimeout(function () {
      laser.off()
    }, 500)
  }

  io.on("connection", function (socket) {
    console.log("Client connected")

    socket.on("x", function (x) {
      fireLaser()
      hoz.to(x)
    })

    socket.on("y", function (y) {
      fireLaser()
      vert.to(y)
    })
  })
})

server.listen(8080)
