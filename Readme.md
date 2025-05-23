# Fork Notes

This is a fork of [py-obsidianmd](https://github.com/selimrbd/py-obsidianmd) by selimrbd. As far as I can tell, selimrbd is not developing py-obsidianmd, so I am fixing bugs and adding features to suit my needs.

Change Log (newest to oldest):
- Bug fix: Leverage yaml.dump from the pyYaml library to ensure that characters are properly escaped.
- Bug fix: Maintain quotes around frontmatter property values that contain ': '. (a colon followed by a space.)
- New Feature: Added parameter `excludePaths` to Notes.__init__. This is a pathlib.Path object (or a list of them). If excludePaths are sub-directories of the `paths` parameter, the sub-directories will be excluded from the batch.
- Bug fix: Maintain quotes around internal link property values. The quotes are necessary for Obsidian to parse internal links in properties. Obsidian includes them automatically, but py-obsidianmd was stripping them out.


# py-obsidianmd

A python library for modifying [Obsidian](https://obsidian.md/) notes in batch.

See the [full documentation](https://selimrbd.github.io/py-obsidianmd/)

:warning: **Consider backing up your vault** before using the library, to avoid any risk of data loss. You can test the library on this [example vault](https://github.com/selimrbd/example-vault)



## Presentation video

[![Watch the video](https://img.youtube.com/vi/gRPBAKiu37Y/hqdefault.jpg)](https://www.youtube.com/watch?v=gRPBAKiu37Y)

## Quickstart

```bash
pip install py-obsidianmd
```

```python
from pathlib import Path
from pyomd import Notes
from pyomd.metadata import MetadataType

path_dir = Path('/path/to/obsidian/folder')
notes = Notes(path_dir)
```

## move metadata between frontmatter and inline

```python
notes.metadata.move(fr=MetadataType.FRONTMATTER, to=MetadataType.INLINE)
notes.update_content(inline_inplace=False, inline_position="top", inline_tml="standard") #type: ignore
notes.write()
```
![](./docs/docs/assets/example-gifs/pyomd-1.gif)

## regroup inline metadata inside a callout

```python
notes.update_content(inline_inplace=False, inline_position="top", inline_tml="callout") #type: ignore
notes.write()
```
![](./docs/docs/assets/example-gifs/pyomd-2.gif)

## add and remove metadata 
```python
notes.filter(has_meta=[("tags", "type/book", MetadataType.INLINE)])

notes.metadata.add(k="type", l="[[book]]", meta_type=MetadataType.INLINE)
notes.metadata.remove(k="tags", l="type/book", meta_type=MetadataType.INLINE)

notes.update_content(inline_inplace=False, inline_position="top", inline_tml="callout") #type: ignore
notes.write()
```
![](./docs/docs/assets/example-gifs/pyomd-3.gif)

## License

[BSD 3](LICENSE.txt)

## Contributing
Contributions are welcome ! Different ways you can contribute:
- **Write an issue**: report a bug, suggest an enhancement, ...
- **Submit a pull request** to solve an open issue

For more details, see the [contribution guidelines](CONTRIBUTING.md).

## Support

If you found this library useful and wish to support it's development, you can do so using the links below (paypal or Ko-fi). Thanks a bunch !

<a href="https://www.paypal.com/donate/?hosted_button_id=R5NYTS46CQMSS"><img src="./docs/docs/assets/donate-paypal.png" width="150" height="100" /></a>
<br>
<a href="https://ko-fi.com/selimrbd"><img src="./docs/docs/assets/donate-kofi.png" width="200" height="50" /></a>
