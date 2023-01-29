### Config, initialization and run

To config this and prepare its execution, run

```
cargo build --release
cp target/release/handler .
```

Open `host.json` and inside `customHandler` > `description` > `defaultExecutablePath` write the name of the folder that contains the file `function.json` (add .exe if you're on windows)

Run the function with `func start`. Be sure to have installed [Func 3.x](https://learn.microsoft.com/it-IT/azure/azure-functions/functions-run-local?tabs=v4%2Cwindows%2Ccsharp%2Cportal%2Cbash#v2)

Go to this URL and see the function working (http://localhost:7071/api/HttpExample?name=Functions)

To deploy, create a file `.cargo/config`, and write this inside it:
```
[target.x86_64-unknown-linux-musl]
linker = "rust-lld"
```

Then, run these 3 commands (*)
```
rustup target add x86_64-unknown-linux-musl
cargo build --release --target=x86_64-unknown-linux-musl
cp target/x86_64-unknown-linux-musl/release/handler .
```

If you are on a Windows system, the latter will cause issues. Manually copy the file and rename it according to your needs/likings

Eventually, where you had the `host.json` file and you wrote the name of the folder, now write the name of the latest copied file (without .exe)