Chisel 3 supports multiple clock domains as follows.

Note that in order to cross clock domains safely, you will need appropriate synchronization logic (such as an asynchronous FIFO).

```scala
class MultiClockModule extends Module {
  val io = IO(new Bundle {
    val clockB = Input(Clock())
    val stuff = Input(Bool())
  })

  // This register is clocked against the module clock.
  val regClock = RegNext(stuff)

  withClock (io.clockB) {
    // In this withClock scope, all synchronous elements are clocked against io.clockB.

    // This register is clocked against io.clockB.
    val regClockB = RegNext(stuff)
  }

  // This register is also clocked against the module clock.
  val regClock2 = RegNext(stuff)
}
```

[Prev(Polymorphism and Parameterization)](Polymorphism-and-Parameterization) [Next(Chisel3 vs Chisel2)](Chisel3-vs-Chisel2)
