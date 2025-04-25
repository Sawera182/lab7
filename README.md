import 'package:flutter/material.dart';

void main() {
  runApp(MyTimerApp());
}

class MyTimerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TimerScreen(),
    );
  }
}

class TimerScreen extends StatefulWidget {
  @override
  _TimerScreenState createState() => _TimerScreenState();
}

class _TimerScreenState extends State<TimerScreen> {
  int countdown = 10;
  bool isRunning = false;

  void startTimer() async {
    setState(() {
      isRunning = true;
      countdown = 10;
    });

    while (countdown > 0) {
      await Future.delayed(Duration(seconds: 1));
      setState(() {
        countdown--;
      });
    }

    setState(() {
      isRunning = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Timer App")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              '$countdown',
              style: TextStyle(fontSize: 60, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: isRunning ? null : startTimer,
              child: Text("Start Timer"),
            ),
          ],
        ),
      ),
    );
  }
}
