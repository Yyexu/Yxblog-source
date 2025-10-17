---
title: Hello World ，Fuck you
cover: /images/web/30.jpg.jpeg
tags:
  - 编程
  - 电脑
categories:
  - 编程
date: 2025-08-15 17:58:57
---
欢迎来到我的博客

## Quick Start

### Create a new post

```bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

Times New Roman

### Run server

```bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

```bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

```bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

```kotlin
import org.bukkit.Bukkit
import org.bukkit.configuration.ConfigurationSection
import org.bukkit.plugin.java.JavaPlugin
import org.bukkit.event.EventHandler
import org.bukkit.event.Listener
import org.bukkit.inventory.InventoryHolder
import net.kyori.adventure.text.Component
import org.bukkit.Material
import org.bukkit.entity.Player
import org.bukkit.event.inventory.InventoryClickEvent
import org.bukkit.inventory.Inventory
import org.bukkit.inventory.ItemStack

//主程序
class Main:JavaPlugin() {
    override fun onEnable() {
        saveDefaultConfig()
        if(config.getBoolean("enabled",true)){
            server.pluginManager.registerEvents(EventHandlers(config),this)
        }
        println("[Start-menu] 插件已经加载！")
    }
}
//事件类
class EventHandlers(private val config: ConfigurationSection): Listener{
    @EventHandler
    fun onInventoryClick(ev: InventoryClickEvent) {
        //获得物品栏
        val iv = ev.clickedInventory ?: return
        //判断物品栏拥有者是不是 方法 StartMenuInventoryHolder
        if(iv.holder is StartMenuInventoryHolder){
            val clicker = ev.whoClicked as? Player ?: return
            val item = ev.currentItem ?: return
            ev.isCancelled = true
            when(item.type){
                Material.BARRIER -> clicker.health = 0.0
                Material.FIREWORK_ROCKET -> {
                    val vac = clicker.velocity
                    vac.y += config.getDouble("liftoff", 5.0)
                    clicker.velocity = vac
                }
                Material.COMPASS -> {
                    clicker.sendMessage { Component.text("Ping: ${clicker.ping}ms") }
                }
                Material.COMMAND_BLOCK -> {
                    clicker.performCommand(config.getString("command.run","help")!!)
                }
                else -> {}
            }

            iv.close()
        }
    }
}
//开始菜单的创建，拥有者
class StartMenuInventoryHolder(config: ConfigurationSection): InventoryHolder{
    private val inventory = Bukkit.createInventory(this,1 * 9, Component.text("开始菜单"))
        init {
            inventory.addItem(
                makeButton(Material.BARRIER, "重新部署"),
                makeButton(Material.FIREWORK_ROCKET, "快速起飞"),
                makeButton(Material.COMPASS, "查询延迟"),
                makeButton(Material.COMMAND_BLOCK, config.getString("command.label", "执行命令")!!)
            )
        }
    override fun getInventory(): Inventory = inventory
}
//添加按钮 方法
fun makeButton(met: Material,label:String): ItemStack {
    val item = ItemStack(met,1)
    val mata = item.itemMeta
    mata.customName(Component.text(label))
    item.itemMeta = mata
    return item
}
```
