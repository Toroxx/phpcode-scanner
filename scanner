#Author: Lawrence Lau
#Email: m@torolab.hk
#Version: 0.1

import sys, os

file_ext = [".php", ".class"]
search_type = ["istart", "iend", "eval(", "base64_decode(", "base64_encode("]

def is_file_ext(file, exts):
    o = False
    for ext in exts:
        if file.endswith(ext):
            return True
    return False


def dir_lookup(path, file_list, exts):
    for file in os.listdir(path):
        tpath = path + file

        if os.path.isdir(tpath):
            file_list = dir_lookup(tpath + "/", file_list, exts)
        else:
            if is_file_ext(file, exts):
                if tpath not in file_list:
                    file_list.append(tpath)

    return file_list


def search_data(filename, test):
    fount_line = []
    counter = {'count': 0, 'lines': []}
    i = 0
    with open(filename) as f:
        for line in f.readlines():
            i += 1
            for test_str in test:
                tline = line.replace("\n", "")
                if tline.find(test_str) > -1:
                    if i not in fount_line:
                        counter['count'] += 1
                        fount_line.append(i)
                        counter['lines'].append("line {0}: {1}".format(i, tline))

    return counter


# -------------------------------------------------------


if len(sys.argv) == 2:
    path = sys.argv[1]
else:
    print("Please enter path")
    sys.exit()

print("Scan start \n-------------------------------------")

file_list = []
file_list = dir_lookup(path, file_list, file_ext)

for file in file_list:
    txt = search_data(file, search_type)
    if txt['count'] > 0:
        print("File: {0}, found: {1}".format(file, txt["count"]))
        for fline in txt['lines']:
            print(fline)
        print("")

print("End for scan")
