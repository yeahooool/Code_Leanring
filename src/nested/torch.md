# import torch

1. `torch.zeros_like(Tensor, dtype)`: 返回一个为 0 的 Tensor.

<<<<<<< HEAD
2. `torch.set_printoptions()`: 显示的元素精度
=======
2. `torch.set_printoptions()`: 显示的元素精度。
>>>>>>> 3a98cd2 (update)
    <details>
    <summary>详细解释</summary>
    
    ```python
    def set_printoptions(
        precision=None,
        threshold=None,
        edgeitems=None,
        linewidth=None,
        profile=None,
        sci_mode=None,
    ):
        r"""Set options for printing. Items shamelessly taken from NumPy
    
        Args:
            precision: Number of digits of precision for floating point output
                (default = 4).
            threshold: Total number of array elements which trigger summarization
                rather than full `repr` (default = 1000).
            edgeitems: Number of array items in summary at beginning and end of
                each dimension (default = 3).
            linewidth: The number of characters per line for the purpose of
                inserting line breaks (default = 80). Thresholded matrices will
                ignore this parameter.
            profile: Sane defaults for pretty printing. Can override with any of
                the above options. (any one of `default`, `short`, `full`)
            sci_mode: Enable (True) or disable (False) scientific notation. If
                None (default) is specified, the value is defined by
                `torch._tensor_str._Formatter`. This value is automatically chosen
                by the framework.
    
        Example::
    
            >>> # Limit the precision of elements
            >>> torch.set_printoptions(precision=2)
            >>> torch.tensor([1.12345])
            tensor([1.12])
            >>> # Limit the number of elements shown
            >>> torch.set_printoptions(threshold=5)
            >>> torch.arange(10)
            tensor([0, 1, 2, ..., 7, 8, 9])
            >>> # Restore defaults
            >>> torch.set_printoptions(profile='default')
            >>> torch.tensor([1.12345])
            tensor([1.1235])
            >>> torch.arange(10)
            tensor([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
    
        """
        if profile is not None:
            if profile == "default":
                PRINT_OPTS.precision = 4
                PRINT_OPTS.threshold = 1000
                PRINT_OPTS.edgeitems = 3
                PRINT_OPTS.linewidth = 80
            elif profile == "short":
                PRINT_OPTS.precision = 2
                PRINT_OPTS.threshold = 1000
                PRINT_OPTS.edgeitems = 2
                PRINT_OPTS.linewidth = 80
            elif profile == "full":
                PRINT_OPTS.precision = 4
                PRINT_OPTS.threshold = inf
                PRINT_OPTS.edgeitems = 3
                PRINT_OPTS.linewidth = 80
    
        if precision is not None:
            PRINT_OPTS.precision = precision
        if threshold is not None:
            PRINT_OPTS.threshold = threshold
        if edgeitems is not None:
            PRINT_OPTS.edgeitems = edgeitems
        if linewidth is not None:
            PRINT_OPTS.linewidth = linewidth
        PRINT_OPTS.sci_mode = sci_mode
    ```
<<<<<<< HEAD
    </details>
=======
    </details>

3. `import torch.backends.cudnn as cudnn`: 为什么使用相同的网络结构，跑出来的效果完全不同，用的学习率，迭代次数，batch size 都是一样？固定随机数种子是非常重要的。但是如果你使用的是PyTorch等框架，还要看一下框架的种子是否固定了。还有，如果你用了cuda，别忘了cuda的随机数种子。这里还需要用到torch.backends.cudnn.deterministic.

    `torch.backends.cudnn.deterministic`是啥？顾名思义，将这个 flag 置为`True`的话，每次返回的卷积算法将是确定的，即默认算法。如果配合上设置 Torch 的随机种子为固定值的话，应该可以保证每次运行网络的时候相同输入的输出是固定的，代码大致这样:
    ```python
    def init_seeds(seed=0):
    torch.manual_seed(seed) # sets the seed for generating random numbers.
    torch.cuda.manual_seed(seed) # Sets the seed for generating random numbers for the current GPU. It’s safe to call this function if CUDA is not available; in that case, it is silently ignored.
    torch.cuda.manual_seed_all(seed) # Sets the seed for generating random numbers on all GPUs. It’s safe to call this function if CUDA is not available; in that case, it is silently ignored.

    if seed == 0:
        cudnn.deterministic = True
        cudnn.benchmark = False
    ```
    > `torch.backends.cudnn.benchmark = true`: 大部分情况下，设置这个 flag 可以让内置的 cuDNN 的 auto-tuner 自动寻找最适合当前配置的高效算法，来达到优化运行效率的问题。<br>
    > 一般来讲，应该遵循以下准则：    
    > * 如果网络的输入数据维度或类型上变化不大，设置  `torch.backends.cudnn.benchmark = true`  可以增加运行效率；
    > * 如果网络的输入数据在每次 iteration 都变化的话，会导致 cnDNN 每次都会去寻找一遍最优配置，这样反而会降低运行效率。
    > * 为了避免计算结果的波动，设置`torch.backends.cudnn.deterministic = True`.

4. 
>>>>>>> 3a98cd2 (update)
