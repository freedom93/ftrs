## [避免使用有损编解码器重新压缩图像](https://images.guide/#avoid-recompressing-images-lossy-codecs)

建议始终对原始图像进行压缩。重新压缩图像会有后果。假设您有一个JPEG，它已经被压缩，质量为60。如果您用有损编码重新压缩此图像，它看起来会更糟。每一轮额外的压缩都将引入分代丢失——信息将丢失，压缩工件将开始构建。即使你在高质量的环境下重新压缩。

为了避免这个陷阱，**首先设置您愿意接受的最低质量的文件**，您将从一开始就获得最大的文件节省。然后您就可以避免这个陷阱，因为仅从降低质量的角度来看，任何文件大小的减少都是不好的。

重新编码一个有损耗的文件几乎总是会得到一个较小的文件，但这并不意味着您可以从中获得您可能认为的那么多的质量。

![Performance](https://images.guide/images/book-images/generational-loss-large.jpg)

上面，从Jon Sneyers的这段[优秀的视频](https://www.youtube.com/watch?v=w7vXJbLhTyI)和[附带的文章](http://cloudinary.com/blog/why_jpeg_is_like_a_photocopier)中，我们可以看到使用几种格式进行重新压缩的世代损失影响。如果从社交网络中保存(已压缩)图像并重新上传(导致重新压缩)，您可能会遇到这个问题。质量损失会增加。

由于网格量化，MozJPEG（可能是偶然的）对再压缩降级具有更好的抵抗力。 它不是精确地压缩所有DCT值，而是检查+1/-1范围内的接近值，以查看类似值是否压缩为更少的位。有损FLIF有一个类似于有损PNG的hack，在(重新)压缩之前，它可以查看数据并决定丢弃什么。重新压缩的png有“漏洞”，它可以检测，以避免进一步改变数据。

**在编辑源文件时，以无损的格式(如PNG或TIFF)存储它们，以便尽可能地保持质量。**然后，您的构建工具或图像压缩服务将以最小的质量损失向用户输出您所服务的压缩版本。