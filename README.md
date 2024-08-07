# My Conky Config

```config
conky.config = {
	update_interval = 1,
	cpu_avg_samples = 2,
	net_avg_samples = 2,
	out_to_console = false,
	override_utf8_locale = true,
	double_buffer = true,
	no_buffers = true,
	text_buffer_size = 32768,
	imlib_cache_size = 0,
	own_window = true,
	own_window_type = 'normal',
	own_window_argb_visual = false,
	own_window_argb_value = 175,
	own_window_hints = 'undecorated,below,sticky,skip_taskbar,skip_pager',
	border_inner_margin = 5,
	border_outer_margin = 0,
	gap_x = 6,
	gap_y = 0,
 	draw_shades = false,
	draw_outline = false,
	draw_borders = false,
	draw_graph_borders = false,
	use_xft = true,
	xftalpha = 0.8,
	uppercase = false,
	default_color = 'green',
    own_window_colour = '#000000',
	minimum_width = 320, minimum_height = 0,
	alignment = 'top_right',
};

conky.text = [[
${voffset 0}${font sans-serif:bold:size=15}${alignc}${time %H:%M}${font}
${voffset 5}${alignc}${time %A, %d de %B de %Y}
${font sans-serif:bold:size=10}SYSTEM ${hr 2}
${font sans-serif:normal:size=9}$sysname $kernel $alignr $machine
Distro:$alignr ${execi 1000 ( lsb_release -ds || cat /etc/*release || uname -om ) 2>/dev/null | head -n1}
Host:$alignr$nodename
Uptime:$alignr$uptime
File System: $alignr${fs_type}
Processes: $alignr ${execi 1000 ps aux | wc -l}

${font sans-serif:bold:size=10}GPU ${hr 2}
${font sans-serif:normal:size=9}Model $alignr ${exec nvidia-smi --query-gpu=gpu_name --format=csv,noheader,nounits} (v${exec nvidia-smi --query-gpu=driver_version --format=csv,noheader,nounits})
Temperature $alignr ${execi 1 nvidia-settings -query [gpu:0]/GPUCoreTemp -t} °C
GPU Utilization $alignr ${execi 1 nvidia-smi --query-gpu=utilization.gpu --format=csv,noheader,nounits} %
VRAM Utilization $alignr ${execi 1 nvidia-smi --query-gpu=memory.used --format=csv,noheader,nounits} Mb / ${execi 1 nvidia-smi --query-gpu=memory.total --format=csv,noheader,nounits } MB
VRAM Free $alignr ${execi 1 nvidia-smi --query-gpu=memory.free --format=csv,noheader,nounits} MB
Clocks SM Utilization $alignr ${execi 1 nvidia-smi --query-gpu=clocks.current.sm --format=csv,noheader,nounits} Mhz
Watts $alignr ${execi 1 nvidia-smi --query-gpu=power.draw --format=csv,noheader,nounits}
Fan Speed $alignr ${execi 1 nvidia-smi --query-gpu=fan.speed --format=csv,noheader,nounits} %

${font sans-serif:bold:size=10}CPU ${hr 2}
${font sans-serif:normal:size=9}${execi 1000 grep model /proc/cpuinfo | cut -d : -f2 | tail -1 | sed 's/\s//'}
CPU Usage: $cpu% ${cpubar 11,0}

${font sans-serif:bold:size=10}MEMORY ${hr 2}
${font sans-serif:normal:size=8}RAM $alignc $mem / $memmax $alignr $memperc%
$membar

${font sans-serif:bold:size=10}DISK USAGE ${hr 2}
${font sans-serif:normal:size=8}/ $alignc ${fs_used /} / ${fs_size /} $alignr ${fs_used_perc /}%
${fs_bar /}
${voffset 2}${font sans-serif:normal:size=8}/home $alignc ${fs_used /home} / ${fs_size /home} $alignr ${fs_used_perc /home}%
${fs_bar /home}
${voffset 2}${font sans-serif:normal:size=8}/data $alignc ${fs_used /data} / ${fs_size /data} $alignr ${fs_used_perc /data}%
${fs_bar /data}

${font sans-serif:bold:size=10}NETWORK ${hr 2}
${font sans-serif:normal:size=8}Local IPs:${alignr}External IP:
${execi 1000 ip a | grep inet | grep -vw lo | grep -v inet6 | cut -d \/ -f1 | sed 's/[^0-9\.]*//g' | head -1} ${alignr}${execi 1000  wget -q -O- http://ipecho.net/plain; echo}
${font sans-serif:normal:size=8}Down: ${downspeed eno1}  ${alignr}Up: ${upspeed eno1}

${font sans-serif:bold:size=10}TOP PROCESSES ${hr 2}
${font sans-serif:normal:size=9}Name $alignr PID   CPU%   MEM%${font sans-serif:normal:size=9}
${top name 1} $alignr ${top pid 1} ${top cpu 1}% ${top mem 1}%
${top name 2} $alignr ${top pid 2} ${top cpu 2}% ${top mem 2}%
${top name 3} $alignr ${top pid 3} ${top cpu 3}% ${top mem 3}%
${top name 4} $alignr ${top pid 4} ${top cpu 4}% ${top mem 4}%
${top name 5} $alignr ${top pid 5} ${top cpu 5}% ${top mem 5}%
${top name 6} $alignr ${top pid 6} ${top cpu 6}% ${top mem 6}%
${top name 7} $alignr ${top pid 7} ${top cpu 7}% ${top mem 7}%
${top name 8} $alignr ${top pid 8} ${top cpu 8}% ${top mem 8}%
${top name 9} $alignr ${top pid 9} ${top cpu 9}% ${top mem 9}%
${top name 10} $alignr ${top pid 10} ${top cpu 10}% ${top mem 10}%
]];
```
