Sample usage:

1. Insert files into tar stream, reading from src and writing to dst

        ```python
        # open src file, can be a socket
        src_fp = open(src, 'rb')
        # open dst file, can be a socket
        dst_fp = open(dst, 'wb')
        # list of files we want to insert, wrapped with iterator/reader
        path_list = [RegFile(path, chunk_size) for path in path_list]
        # iterating over resulting stream and writing it to dst socket/file
        for data in TarStream(src_fp, path_list, chunk_size):
            dst_fp.write(data)
        ```

2. Extract specific file names/paths from the stream, leaving the stream intact

        ```python
        # open dst file, can be a socket
        dst_fp = open(dst, 'wb')
        # list of destination files, or, you've guessed it, sockets
        path_list = [open(path, 'wb') for path in path_list]
        # creating iterator from src file
        src_iter = RegFile(src, chunk_size)
        # iterating over resulting stream and writing it to dst socket/file
        for data in UntarStream(src_iter, path_list):
            dst_fp.write(data)
        ```
