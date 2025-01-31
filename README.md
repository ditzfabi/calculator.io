import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Calculadora Web',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Calculadora(),
    );
  }
}

class Calculadora extends StatefulWidget {
  @override
  _CalculadoraState createState() => _CalculadoraState();
}

class _CalculadoraState extends State<Calculadora> {
  String _output = '0';
  String _input = '';
  
  void _onButtonPressed(String value) {
    setState(() {
      if (value == 'C') {
        _input = '';
        _output = '0';
      } else if (value == '=') {
        try {
          _output = _calculate(_input);
        } catch (e) {
          _output = 'Erro';
        }
      } else {
        _input += value;
        _output = _input;
      }
    });
  }

  String _calculate(String expression) {
    // Aqui você pode usar uma expressão regular para avaliar a operação.
    // O método abaixo usa o pacote `expressions` ou `math_expressions` para uma solução mais robusta
    // Para simplificar, vamos usar a função eval, mas cuidado com a segurança ao usar ela em produção.

    // No exemplo básico, usamos um pacote como math_expressions para fazer os cálculos
    return expression; // Substitua com uma lógica de cálculo real
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Calculadora Web'),
      ),
      body: Padding(
        padding: EdgeInsets.all(20),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            // Exibe o resultado
            Text(
              _output,
              style: TextStyle(fontSize: 40, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 20),
            // Exibe os botões da calculadora
            GridView.builder(
              gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 4,
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
              ),
              itemCount: 16,
              shrinkWrap: true,
              itemBuilder: (context, index) {
                final buttons = [
                  '7', '8', '9', '/',
                  '4', '5', '6', '*',
                  '1', '2', '3', '-',
                  'C', '0', '=', '+',
                ];
                return ElevatedButton(
                  onPressed: () => _onButtonPressed(buttons[index]),
                  child: Text(
                    buttons[index],
                    style: TextStyle(fontSize: 24),
                  ),
                );
              },
            ),
          ],
        ),
      ),
    );
  }
}
