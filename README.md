# TensorSlow
## Uma re-implementação do <a href="http://www.tensorflow.org">TensorFlow</a> funcionalmente em python puro

TENSOR-SLOW é um API minimalista de Aprendizado de Máquina que imita a API do TENSOR-FLOW, porém é implementada em Python 3.7 puro (sem o back-end em C). O código fonte foi escrito para maximizar o entendimento das abstrações e detrimento da máxima eficiência performática. Contudo, TensorSlow deve ser utilizado para propósitos educacionais. Se você deseja entender como Bibliotecas como o TensorFlow são por de debaixo do capô, aqui está uma oportunidade.

Detalhes da produção original deste repositório, em inglês: <a href="http://www.deepideas.net/deep-learning-from-scratch-theory-and-implementation/">deepideas.net</a> 
Detalhes do desenvolvimento da biblioteca orginal em inglês:<a href="http://www.deepideas.net/deep-learning-from-scratch-theory-and-implementation/">Deep Learning From Scratch</a>.

## Como Utilizar:
Import:
    import tensorslow as ts

Create a computational graph:

    ts.Graph().as_default()

Create input placeholders:

    training_features = ts.placeholder()
    training_classes = ts.placeholder()

Build a model:

	weights = ts.Variable(np.random.randn(2, 2))
	biases = ts.Variable(np.random.randn(2))
	model = ts.softmax(ts.add(ts.matmul(X, W), b))

Create training criterion:

    loss = ts.negative(ts.reduce_sum(ts.reduce_sum(ts.multiply(training_classes, ts.log(model)), axis=1)))

Create optimizer:

    optimizer = ts.train.GradientDescentOptimizer(learning_rate=0.01).minimize(J)

Create placeholder inputs:

	feed_dict = {
		training_features: my_training_features,
		training_classes: my_training_classes
	}

Create session:

	session = ts.Session()

Train:

	for step in range(100):
		loss_value = session.run(loss, feed_dict)
		if step % 10 == 0:
			print("Step:", step, " Loss:", loss_value)
		session.run(optimizer, feed_dict)

Retrieve model parameters:

	weights_value = session.run(weigths)
	biases_value = session.run(biases)

Check out the `examples` directory for more.
