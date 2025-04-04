# proj287-Android-performance-analysis-tool

## Android Performance Analysis Tool Based on eBPF and Perfetto
## 基于eBPF和Perfetto的Android性能分析工具

## Project Source
## 项目来源

https://github.com/oscomp/proj287-Android-performance-analysis-tool.git

## Project Description
## 项目描述

- Perfetto

Perfetto is now an indispensable general-purpose performance monitoring and tracing tool in the Android platform. It can intuitively present collected data such as Linux kernel ftrace events, perf events, Android atrace events, and logcat in a Web UI, greatly facilitating the analysis and location of performance issues on the Android platform.

Perfetto当前已经是Android平台中不可或缺的一种通用性能检测和跟踪分析工具，其可以将采集到的Linux kernel ftrace events、perf events、Android atrace events、logcat等数据直观呈现在Web UI中，极大地方便了Android平台性能问题的分析与定位。

- eBPF

eBPF is a currently very popular Linux kernel observability technology that provides the ability to observe the kernel through injection without modifying the Kernel code. It has a large community support and excellent development prospects. The new version of Android has integrated the core functions of libbpf-CORE, and the standard kernel supported by GKI has also enabled BPF-related configurations.

eBPF是一种当前非常热门的Linux内核可观测技术，它提供了一种在不修改Kernel代码的情况下，通过注入的方式对内核进行观测的能力，有庞大的社区支撑，极好的发展前景。新版的Android已经集成了libbpf-CORE相关核心功能，GKI支持的标准内核也均以启用了BPF相关配置。

Many applications in the Android system create a large number of threads frequently to perform some asynchronous operations, which brings considerable load pressure to CPU scheduling. This project aims to track thread creation from the source, such as which application/process, which thread, which user-mode call stack created it, and the thread's lifetime. By categorizing and analyzing these data, we can locate unreasonable thread creation code and guide application developers to optimize.

Android系统中很多应用会大量、频繁地创建线程来执行一些异步操作，这给CPU调度带来不少负载压力。本课题希望从源头上跟踪线程创建，比如哪个应用/进程、哪个线程、哪个用户态调用栈创建的，线程存活时间，通过对这些数据进行归类分析，来定位不合理的线程创建代码，引导应用开发者进行优化。

These data can be presented in the console with statistical results in different dimensions such as frequency, quantity, call stack, survival time, parent thread name, application name, etc.; key indicator data can also be written to Perfetto and finally presented in the Perfetto UI.

这些数据可以在控制台中通过频度、数量、调用栈、存活时间、父线程名、应用名等不同维度展现统计结果；也可以将关键指标数据写入Perfetto，最终在Perfetto UI中呈现；

In the Android system, threads often enter the D state due to IO, low memory, or other reasons, causing UI display and composition processes to be blocked, resulting in stuttering. This project aims to mark threads entering the D state with their kernel + user-mode call stacks in the Perfetto UI.

Android系统中经常会有线程因IO、低内存或者其他原因进入D状态，导致UI显示、合成流程被阻塞，造成卡顿，本课题希望在Perfetto UI中对进入D状态的线程标记出其内核+用户态调用栈；

The requirements for Kernel/user-mode call stacks in the above topics: at least 6 levels of call stacks from the target function upwards, and the kernel/user-mode call stack display must be accurate (correctly parse symbols in Android odex/oat files).

以上课题对Kernel/用户态调用栈要求：从目标函数开始往上算起至少包含6级调用栈，内核态/用户态调用栈显示要准确 (正确解析Android odex/oat文件中的符号)。

## Reference Materials
## 已有参考资料

- Perfetto Analysis ([Introduction](https://perfetto.dev/docs/), [Advanced](https://mp.weixin.qq.com/s/gXNm24I1qFw-xRhQC-Zsow));
- Perfetto分析（[简介](https://perfetto.dev/docs/)，[进阶](https://mp.weixin.qq.com/s/gXNm24I1qFw-xRhQC-Zsow)）；
- [eBPF Practice on the Android Platform](https://www.bilibili.com/video/BV1wY411f7aM/?p=6)
- [eBPF在Android平台的实践](https://www.bilibili.com/video/BV1wY411f7aM/?p=6)

## License

Apache-2.0 or BSD-2