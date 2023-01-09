### brew services报错

今天在使用brew services启动nginx服务的时候报错了。

环境/系统：MacPro M1，MacOS Ventura 13.1

前段时间系统升级过级，我印象中是在系统升级之前使用brew services指令是正常的。我虽然不经常使用nginx，但是也经常做一些测试啥的，之前的功能是正常的。大概的报错信息如下：

```bash
[xxxxxxxxx ~]$ brew services
Error: undefined method `launchd_service_path' for #<Formulary::FormulaNamespace1db1b67abc150bcac6739031eda6c7db::Tree:0x00007fa9a693d8c8>
/opt/homebrew/Library/Taps/homebrew/homebrew-services/lib/service/formula_wrapper.rb:58:in `service_file'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/lib/service/formula_wrapper.rb:92:in `plist?'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/lib/service/formulae.rb:12:in `select'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/lib/service/formulae.rb:12:in `available_services'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/lib/service/formulae.rb:17:in `services_list'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/lib/service/commands/list.rb:13:in `run'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/cmd/services.rb:102:in `services'
/opt/homebrew/Library/Homebrew/brew.rb:93:in `<main>'
```

看到报错信息后，具体原因不太明确，但是可以明确的是homebrew-services出问题了。

确认了问题后，我的解决方案是将homebrew-services目录直接删除掉，然后更新下该服务。

切换到/opt/homebrew/Library/Taps/homebrew目录，因为根据报错信息，是这个目录的homebrew-services出了问题

```bash
cd /opt/homebrew/Library/Taps/homebrew

# 移除掉homebrew-services
rm -rf homebrew-services

# 更新homebrew-services
brew tap homebrew/services
```

经过上述的操作之后，brew services服务恢复正常，可以正常使用了。

> 由于最近更新了MacOS的版本，从之前的版本12更新到了13.1，更新后到现在已经发现了2个问题了。第一个问题是git的使用出了问题，再就是今天的这个brew services的使用出了问题。至于还有没有其他的问题出现，现在还不确定。

由于MacOS系统的升级，导致了git、homebrew使用上的问题，以及Mac本身芯片的不同，有intel和M系列的，不同的芯片驱动又有不同，导致初次在使用一些开发工具的时候有点麻烦，带来了开发上非常不爽的体验。再就是，系统谨慎升级。升级系统，感觉就是在给自己挖坑。因为我不知道系统升级后会有什么问题在前面等着呢。