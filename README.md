This is official Impulse neural network library repository.

You can do this with it and more.
```java
ArrayList<Layer> layers = new ArrayList<Layer>();

layers.add(new Input(3, 150, 150));
layers.add(new Conv2D(32, 3, 1, 0, Activation.RELU, true, new Glorot()));
layers.add(new MaxPool2D(2, 2));
layers.add(new Conv2D(64, 3, 1, 0, Activation.RELU, true, new Glorot()));
layers.add(new MaxPool2D(2, 2));
layers.add(new Conv2D(128, 3, 1, 0, Activation.RELU, true, new Glorot()));
layers.add(new MaxPool2D(2, 2));
layers.add(new Conv2D(128, 3, 1, 0, Activation.RELU, true, new Glorot()));
layers.add(new MaxPool2D(2, 2));
layers.add(new Flatten());
layers.add(new Dense(512, Activation.RELU, true, new Glorot()));
layers.add(new Dense(2, Activation.SOFTMAX, true, new Glorot()));
		
Net model = new Net(layers.toArray(new Layer[0]));
model.create();
		
ImageGenerator trainGen = new ImageGenerator("/home/user/Desktop/cats_n_dogs/train",
			150, 150, ImageGenerator.RGB, 0, 255, 100);
ImageGenerator testGen = new ImageGenerator("/home/user/Desktop/cats_n_dogs/validation",
			150, 150, ImageGenerator.RGB, 0, 255, 100);
		
model.fitWithValid(new Adam(0.001f, 0.9f, 0.999f), new CrossEntropy(),
		trainGen, testGen, 100, true);		

float[][] res = model.predict(testGen);
new Matrix(res).print();
```
