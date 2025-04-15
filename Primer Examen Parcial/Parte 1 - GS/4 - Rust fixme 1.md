### Descripción
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/3f0e13f541928f420d9c8c96b06d4dbf7b2fa18b15adbd457108e8c80a1f5883/fixme1.tar.gz).
### Solución
Iniciamos descargando el código de Rust, con ayuda del comando wget:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Ex_1_GS/rust_1]
└─$ wget https://challenge-files.picoctf.net/c_verbal_sleep/3f0e13f541928f420d9c8c96b06d4dbf7b2fa18b15adbd457108e8c80a1f5883/fixme1.tar.gz
--2025-04-08 23:46:09--  https://challenge-files.picoctf.net/c_verbal_sleep/3f0e13f541928f420d9c8c96b06d4dbf7b2fa18b15adbd457108e8c80a1f5883/fixme1.tar.gz
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 65.9.149.59, 65.9.149.85, 65.9.149.24, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|65.9.149.59|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1415 (1.4K) [application/octet-stream]
Saving to: ‘fixme1.tar.gz’

fixme1.tar.gz                100%[=============================================>]   1.38K  --.-KB/s    in 0.003s  

2025-04-08 23:46:10 (434 KB/s) - ‘fixme1.tar.gz’ saved [1415/1415]
```

Una vez que se aprecia que lo descargado viene comprimido con gzip y contenido en un archivo tar, se procede a extraer el contenido con el comando **tar**, y como argumento tiene que se extraiga el contenido del archivo con "x", luego que enliste los archivos que se están extrayendo con "v" y por ultimo que lo descomprima el archivo utilizando gzip con "z", tal como se aprecia a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Ex_1_GS/rust_1]
└─$ tar -xvzf fixme1.tar.gz 
fixme1/
fixme1/Cargo.toml
fixme1/Cargo.lock
fixme1/src/
fixme1/src/main.rs
```

Una vez que hemos acabado de descomprimir y extraer todo el archivo nos cambiamos al directorio **fixme1**, con cd:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Ex_1_GS/rust_1]
└─$ cd fixme1
```

Una vez dentro de ahí, ejecutamos el comando **cargo build**, lo que cual nos permite compilar el proyecto en Rust:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Ex_1_GS/rust_1/fixme1]
└─$ cargo build    
    Updating crates.io index
  Downloaded either v1.13.0
  Downloaded xor_cryptor v1.2.3
  Downloaded crossbeam-deque v0.8.5
  Downloaded crossbeam-epoch v0.9.18
  Downloaded crossbeam-utils v0.8.20
  Downloaded rayon-core v1.12.1
  Downloaded rayon v1.10.0
  Downloaded 7 crates (388.2 KB) in 4.79s
   Compiling crossbeam-utils v0.8.20
   Compiling rayon-core v1.12.1
   Compiling either v1.13.0
   Compiling crossbeam-epoch v0.9.18
   Compiling crossbeam-deque v0.8.5
   Compiling rayon v1.10.0
   Compiling xor_cryptor v1.2.3
   Compiling rust_proj v0.1.0 (/home/kali/notas-hacking/Ex_1_GS/rust_1/fixme1)
error: expected `;`, found keyword `let`
 --> src/main.rs:5:37
  |
5 |     let key = String::from("CSUCKS") // How do we end statements in Rust?
  |                                     ^ help: add `;` here
...
8 |     let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "6...
  |     --- unexpected token

error: argument never used
  --> src/main.rs:26:9
   |
25 |         ":?", // How do we print out a variable in the println function? 
   |         ---- formatting specifier missing
26 |         String::from_utf8_lossy(&decrypted_buffer)
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ argument never used

error[E0425]: cannot find value `ret` in this scope
  --> src/main.rs:18:9
   |
18 |         ret; // How do we return in rust?
   |         ^^^ help: a local variable with a similar name exists: `res`

For more information about this error, try `rustc --explain E0425`.
error: could not compile `rust_proj` (bin "rust_proj") due to 3 previous errors
```

Como podemos ver nos arroja diversos errores en la compilación, es por ello nos vemos obligados a cambiar de directorio, en este caso sería al origen o src:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Ex_1_GS/rust_1/fixme1]
└─$ cd src 
```

Ahora usaremos el editor nano para editar el código y corregir los errores encontrados:

```shell
┌──(kali㉿kali)-[~/…/Ex_1_GS/rust_1/fixme1/src]
└─$ nano main.rs 
```

Una vez cargado obtenemos lo siguiente:

```rust
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS") // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "2>

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        ret; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        ":?", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

Se corrigieron diversos errores, entre ellos puntos y comas, corchetes, corrección en un return y la falta de corchetes, resultando en lo siguiente:

```rust
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS"); // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "2>

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!( 
        "{}:?", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

Como podemos ver, las modificaciones fueron correctas, debido a que desaparecieron los errores y terminó de compilar:

```shell
┌──(kali㉿kali)-[~/…/Ex_1_GS/rust_1/fixme1/src]
└─$ cargo build

   Compiling rust_proj v0.1.0 (/home/kali/notas-hacking/Ex_1_GS/rust_1/fixme1)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 14.10s
```

Por lo que ahora solo queda ejecutarlo con el comando **cargo run**:

```shell
┌──(kali㉿kali)-[~/…/Ex_1_GS/rust_1/fixme1/src]
└─$ cargo run  
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 2.82s
     Running `/home/kali/notas-hacking/Ex_1_GS/rust_1/fixme1/target/debug/rust_proj`
picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}:?
```

Obteniendo así la bandera que soluciona este reto:

```
picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}
```
### Notas Adicionales

### Referencias