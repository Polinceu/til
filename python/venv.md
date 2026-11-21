# Python：venv 虚拟环境，每项目一个，别往全局装包

全局 pip 装一堆包，不同项目要不同版本时迟早打架，venv 是标准库自带的解法。

## 最小流程

```bash
python3 -m venv .venv        # 在项目目录建一个
source .venv/bin/activate    # 激活，提示符前面出现 (.venv)
pip install requests
pip freeze > requirements.txt
deactivate                   # 退出
```

## 容易忘的点

- `.venv` 不要进 git，在 `.gitignore` 里加一行 `.venv/`。
- 换机器恢复环境：`python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt`。
- 提示符没出现 `(.venv)` 就是没激活成功，`which python` 看一眼路径是不是项目下的。
- 系统自带 Python 和项目 Python 版本不一致时，用 `python3.11 -m venv .venv` 指定解释器。
