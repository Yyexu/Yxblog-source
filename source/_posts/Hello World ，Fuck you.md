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

测试标签

{% note default flat %}

你说呢

{% endnote %}

{% note green 'fab fa-internet-explorer' simple %}
前端最讨厌的浏览器
{% endnote %}


{% chartjs 70 %}

<!-- chart -->

{
"type": "line",
"data": {
"labels": ["January", "February", "March", "April", "May", "June", "July"],
"datasets": [{
"label": "My First dataset",
"backgroundColor": "rgb(255, 99, 132)",
"borderColor": "rgb(255, 99, 132)",
"data": [0, 10, 5, 2, 20, 30, 45]
}]
},
"options": {
"responsive": true,
"title": {
"display": true,
"text": "Chart.js Line Chart"
}
}
}

<!-- endchart -->

{% endchartjs %}


{% chartjs %}

<!-- chart -->

{
"type": "radar",
"data": {
"labels": [
"Eating",
"Drinking",
"Sleeping",
"Designing",
"Coding",
"Cycling",
"Running"
],
"datasets": [
{
"label": "My First Dataset",
"data": [65, 59, 90, 81, 56, 55, 40],
"fill": true,
"backgroundColor": "rgba(255, 99, 132, 0.2)",
"borderColor": "rgb(255, 99, 132)",
"pointBackgroundColor": "rgb(255, 99, 132)",
"pointBorderColor": "#fff",
"pointHoverBackgroundColor": "#fff",
"pointHoverBorderColor": "rgb(255, 99, 132)"
},
{
"label": "My Second Dataset",
"data": [28, 48, 40, 19, 96, 27, 100],
"fill": true,
"backgroundColor": "rgba(54, 162, 235, 0.2)",
"borderColor": "rgb(54, 162, 235)",
"pointBackgroundColor": "rgb(54, 162, 235)",
"pointBorderColor": "#fff",
"pointHoverBackgroundColor": "#fff",
"pointHoverBorderColor": "rgb(54, 162, 235)"
}
]
},
"options": {
"elements": {
"line": {
"borderWidth": 3
}
}
}
}

<!-- endchart -->

{% endchartjs %}


{% chartjs 40,true %}

<!-- chart -->

{
"type": "pie",
"data": {
"labels": [
"编程",
"音乐",
"阅读",
"游戏",
"健身",
"旅游"
],
"datasets": [
{
"label": "喜爱指数",
"data": [
30,
24,
19,
14,
9,
4
],
"backgroundColor": {
"dark-mode": [
"rgba(255, 99, 132, 0.5)",
"rgba(54, 162, 235, 0.5)",
"rgba(255, 206, 86, 0.5)",
"rgba(75, 192, 192, 0.5)",
"rgba(153, 102, 255, 0.5)",
"rgba(255, 159, 64, 0.5)"
],
"light-mode": [
"rgba(255, 99, 132, 0.2)",
"rgba(54, 162, 235, 0.2)",
"rgba(255, 206, 86, 0.2)",
"rgba(75, 192, 192, 0.2)",
"rgba(153, 102, 255, 0.2)",
"rgba(255, 159, 64, 0.2)"
]
},
"borderColor": {
"dark-mode": [
"rgba(255, 99, 132, 1)",
"rgba(54, 162, 235, 1)",
"rgba(255, 206, 86, 1)",
"rgba(75, 192, 192, 1)",
"rgba(153, 102, 255, 1)",
"rgba(255, 159, 64, 1)"
],
"light-mode": [
"rgba(255, 99, 132, 1)",
"rgba(54, 162, 235, 1)",
"rgba(255, 206, 86, 1)",
"rgba(75, 192, 192, 1)",
"rgba(153, 102, 255, 1)",
"rgba(255, 159, 64, 1)"
]
}
}
]
},
"options": {
"plugins": {
"legend": {
"labels": {
"color": {
"dark-mode": "rgba(255, 255, 255, 0.8)",
"light-mode": "rgba(0, 0, 0, 0.8)"
}
}
}
}
}
}

<!-- endchart -->

<!-- desc -->

除了**计算机编程**外，我想不出还有其他让我感兴趣的工作。
我可以无中生有地创造出**精美的范式**和**结构**，
在此过程中也解决了无数的小谜团。
<span style="font-size:0.8em;color: var(--sep-secondtext);">I can't think of any other job other than **computer programming** that interests me.
I can create **beautiful paradigms** and **structures** out of nothing,
Countless small mysteries are also solved in the process.</span>

<!-- enddesc -->

{% endchartjs %}


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
