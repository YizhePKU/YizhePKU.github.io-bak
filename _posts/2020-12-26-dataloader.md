# Quick guide to loading data in PyTorch and TensorFlow

## You want `torch.utils.data.Dataloader` and `tf.data.Dataset`

They're convinient tools for proprocessing your data before you feed them into your model. They can

* Split data into batches
* Shuffle data
* Generate new data or transform existing data on the fly

However, I find the official documentation ([here][1] and [here][2]) somewhat unclear.
For example, when and why do you need to specify a buffer size when calling `shuffle()` in TensorFlow?
What is a `map-style dataset` in PyTorch?

This post aims to clarify and provide instructions for common usage.


## Map-style dataset and iterable-style dataset

It's most helpful to catogorize dataset into two types, using terminologies from PyTorch:

* **Map-style datasets** provide random-access capbilities. Examples: Numpy arrays, Python dicts, files on disk
* **Iterable-style dataset** can only be accessed sequentially. Examples: Python generators, streamed data from network

Generally, you should use map-style datasets when possible.
Map-style datasets give you their size ahead of time, are easier to shuffle, and allow for easy parallel loading.

It's a common misconception that if your data doesn't fit in memory, you have to use iterable-style dataset.
That is not true.
You can implement a map-style dataset such that it retrives data as needed.

**tf.data.Dataset only supports iterable-style dataset.**
Once you put data into `tf.data.Dataset`, you can only access it sequentially.
This is also why you have to specify a buffer size when calling `shuffle()`
--there's no easy way to shuffle sequential data without partially saving it in an array.
In this sense, PyTorch is more flexible in handling data loading.


## So how to use them?

If using PyTorch:
* If your data fits in memory(in the form of `np.array`, `torch.Tensor`, or whatever), just pass that to `Dataloader` and you're set.
* If you need to read data incrementally from disk or transform data on the fly, write your own class implementing `__getitem__()` and `__len__()`, then pass that to `Dataloader`.
* If you really have to use iterable-style dataset, write your own class implementing `__iter__()`.

If using TensorFlow:
* If your data fits in memory, my advice is don't bother. It's too much hassle without much benefit.
* Otherwise, follow the [offical guide][3]. Put in your data, then call `batch()`, `shuffle()` and `map()` as necessary.


[1]: https://pytorch.org/docs/stable/data.html
[2]: https://www.tensorflow.org/api_docs/python/tf/data/Dataset
[3]: https://www.tensorflow.org/guide/data
