# import subprocess as sp

1. `sp.check_output()`: Run command with arguments and return its output.
   ```python
   tgt = os.path.join(movement_file, "MOVEMENT")
   res = sp.check_output(["grep", "Iteration", tgt ,"-c"])
   ```
   > grep ... -c 表示出现次数

