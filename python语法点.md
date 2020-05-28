### 读取hdf5文件



```python
#example
f = h5py.File(file_path,'r')
f.keys() #查看文件中的dataset或者group
data = f['xx'][:] #读取key为xx的数据，格式是ndarray
```



### append()和extend()的区别

list.append(object) 向列表中添加一个对象object

```python
music_media = ['compact disc', '8-track tape', 'long playing record']
new_media = ['DVD Audio disc', 'Super Audio CD']
music_media.append(new_media)
print music_media
>>>['compact disc', '8-track tape', 'long playing record', ['DVD Audio disc', 'Super Audio CD']]
```

append()是将内容整体添加到列表的末尾



list.extend(sequence) 把一个序列seq的内容添加到列表中

```python
music_media = ['compact disc', '8-track tape', 'long playing record']
new_media = ['DVD Audio disc', 'Super Audio CD']
music_media.extend(new_media)
print music_media
>>>['compact disc', '8-track tape', 'long playing record', 'DVD Audio disc', 'Super Audio CD']
```

extend()是将内容中的元素逐个添加到list中。



* np.savetxt():将数组保存到txt文件
* np.loadtxt():读取txt文件