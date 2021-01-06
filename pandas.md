# Pandas
[教程](http://yiibai.com/pandas/python_pandas_quick_start.html)
## DataFrame

- 数据操作
    1. 创建
        - df = DataFrame({'column1': [1,2,3], 'column2': [4,5,6]})
        - df = DataFrame([{'c1': 1, 'c2': 4}, {'c1': 2, 'c2': 5}, {'c1': 3, 'c2': 6}])
        - 参数：
            - data
            - index
            - column
            - dtype=np.unit8
            - copy
        - 基础操作
            - ndim
            - shape()
            - size()
            - tail(1)   获取最后一行
            - df.round(3)                  保留小数
            - df.round({'A1': 3, 'B2': 4}) 按列保留小数
            - df['a'].mean()        平均值
            - df.mean()             全列平均值，返回Series
    2. 切片
        ```python

        df.loc[rows, cols]            # 根据index，column， 列可忽略
        df.iloc[row_ids, col_ids]     # 根据行列index       列可忽略
        df.ix[row, col]               # 混合
        df.loc[0, 'c1']
        df.loc[:]
        ```

    3. 遍历
        - 行
        ```python
        for row_id, row in df.iterrows():
            print(row_id)
        ```
        - 列
        ```python
        for col_name, col in df.iteritems():
            print(col_name)
        ```
        - 分组
        ```python
        for key, group in df.groupby('col1'):
            print(key)
            # 每个group是一个 df
        ```

    4. 查找
        ```python
        df[df['列名'] == 'column_value']        # 查询相同字符数据
        df.loc[df['列名'] == 'value']           # 查询相同字符数据
        df[df['列名'].isin(['1', '2'])]         # 查询相同字符串的数据
        df[~df['列名'].isin(['1', '3'])]        # 查询没有相同字符串的数据
        df[(df['列名1'] == 'v1') & (df['age'] > 5)]   # 多条件过滤
        ```
    5. 去重
        ```python
        df.drop_duplicates(['列名1', '列名2'])
        ```
    6. 拼接
        ```python
        df_arr = [df1, df2]
        # 纵向
        df = pd.concat(df_arr)
        # 横向
        df = pd.concat(df_arr, axis=1)


        ```

- 文件操作
    [XlsxWriter库](http://xlsxwriter.readthedocs.io/index.html)
    ```python
    # 读
        df = pd.read_excel('abc.xlsx')
        # 多重索引 前两行和前两列都是索引
        df = pD.read_excel('abc.xlsx', sheet_name='s1', header=[0, 1], index_col=[0,1])

    # 写
        df.to_excel('abc.xlsx')

        writer = pd.ExcelWriter('abc.xlsx', engine='xlswriter')
        df1.to_excel(writer, sheet_name='s1')
        df2.to_excel(writer, sheet_name='s2')
        writer.save()

    # 格式 通过XlsxWriter 库
        wb = writer.book
        sheet1 = writer.sheets['s1']

        # 创建样式
        header_fmt = workbook.add_format({'bold': True, 'fg_color': '#70AD47', 'align': 'center'})
        index_fmt = workbook.add_format({'bold': True})

        # 设置列宽 和样式
        sheet1.set_column(start, end, width, [fmt])
        # 写数据 和样式
        sheet1.write(row, col, value, [fmt])
        # 写入链接
        sheet1.write_url(row, col, value)
    ```
