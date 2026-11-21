<img src="assets/logo.png" width="112" height="112" alt="AckPrefix logo">

# AckPrefix

Find the longest contiguous acknowledgement prefix in unordered deliveries. This Blyx library is part of the queues and messaging collection.

Committing the largest acknowledged offset can skip a message that is still in flight. Advance only through a contiguous prefix. [RabbitMQ, consumer acknowledgements](https://www.rabbitmq.com/docs/confirms)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-ackprefix.git
cd blyx-ackprefix
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-ackprefix) · [Package page](https://www.blyx-lang.space/packages/ackprefix) · [Handbook](https://doc.blyx-lang.space/guide/fulmar)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-ackprefix.git vendor/ackprefix
```

```blyx
use vendor::ackprefix::ackprefix;

fn main() {
    let acked = [5, 7, 5, 4];
    let start = 4.0;
    let result = ackprefix_advance(acked, start);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
6
2
```

## API

`ackprefix_advance(acked, start)`

Returns [next unacknowledged offset, advanced count]. Duplicate acknowledgements never advance the cursor twice. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| acked | Vector of values, each a nonnegative exact integer |
| start | A nonnegative exact integer |

## In use

[Fulmar](https://github.com/Rahulchaube1/blyx-fulmar) uses this module to choose a contiguous commit offset from an out-of-order delivery trace.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-ackprefix/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
