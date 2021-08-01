# My Conky Config

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
    own_window_argb_visual = true,
    own_window_argb_value = 175,
    own_window_hints = 'undecorated,below,sticky,skip_taskbar,skip_pager',
    border_inner_margin = 5,
    border_outer_margin = 0,
    xinerama_head = 1,
    alignment = 'bottom_right',
    gap_x = 0,
    gap_y = 0,
    draw_shades = false,
    draw_outline = false,
    draw_borders = false,
    draw_graph_borders = false,
    use_xft = true,
    font = 'Ubuntu Mono:size=12',
    xftalpha = 0.8,
    uppercase = false,
    default_color = 'green',
    own_window_colour = '#000000',
    minimum_width = 320, minimum_height = 0,
    alignment = 'top_right',

    };
    conky.text = [[

    ${voffset -16}${font sans-serif:bold:size=18}${alignc}${time %H:%M}${font}
    ${voffset 4}${alignc}${time %A %B %d, %Y}
    ${font}${voffset -4}
    ${font sans-serif:bold:size=10}SYSTEM ${hr 2}
    ${font sans-serif:normal:size=9}$sysname $kernel $alignr $machine
    Host:$alignr$nodename
    Uptime:$alignr$uptime
    File System: $alignr${fs_type}
    Processes: $alignr ${execi 1000 ps aux | wc -l}

    ${font sans-serif:bold:size=10}GPU ${hr 2}
    ${font sans-serif:normal:size=9}Model $alignr ${exec nvidia-smi --query-gpu=gpu_name --format=csv,noheader,nounits}
    Temperature $alignr ${execi 60 nvidia-settings -query [gpu:0]/GPUCoreTemp -t} °C
    GPU Utilization $alignr ${exec nvidia-smi | grep % | cut -c 61-63} %
    VRAM Utilization $alignr ${exec nvidia-smi | grep % | cut -c 37-40} MB

    ${font sans-serif:bold:size=12}CPU ${hr 2}
    ${font sans-serif:normal:size=9}${execi 1000 grep model /proc/cpuinfo | cut -d : -f2 | tail -1 | sed 's/\s//'}
    CPU1: ${cpu cpu1}% $alignr ${freq (1)} MHz $alignr ${cpubar cpu1 8,60}
    CPU2: ${cpu cpu2}% $alignr ${freq (2)} MHz $alignr ${cpubar cpu2 8,60}
    CPU3: ${cpu cpu3}% $alignr ${freq (3)} MHz $alignr ${cpubar cpu3 8,60}
    CPU4: ${cpu cpu4}% $alignr ${freq (4)} MHz $alignr ${cpubar cpu4 8,60}
    CPU5: ${cpu cpu5}% $alignr ${freq (5)} MHz $alignr ${cpubar cpu5 8,60}
    CPU6: ${cpu cpu6}% $alignr ${freq (6)} MHz $alignr ${cpubar cpu6 8,60}
    CPU7: ${cpu cpu7}% $alignr ${freq (7)} MHz $alignr ${cpubar cpu7 8,60}
    CPU8: ${cpu cpu8}% $alignr ${freq (8)} MHz $alignr ${cpubar cpu8 8,60}

    ${font sans-serif:bold:size=10}MEMORY ${hr 2}
    ${font sans-serif:normal:size=8}RAM $alignc $mem / $memmax $alignr $memperc%
    $membar
    SWAP $alignc ${swap} / ${swapmax} $alignr ${swapperc}%
    ${swapbar}

    ${font sans-serif:bold:size=10}DISK USAGE ${hr 2}
    ${font sans-serif:normal:size=9}/ $alignc ${fs_used /} / ${fs_size /} $alignr ${fs_used_perc /}%
    ${fs_bar /}

    ${font Ubuntu:bold:size=10}NETWORK ${hr 2}
    ${font sans-serif:normal:size=9}Local IPs:${alignr}External IP:
    ${execi 1000 ip a | grep inet | grep -vw lo | grep -v inet6 | cut -d \/ -f1 | sed 's/[^0-9\.]*//g'}  ${alignr}${execi 1000  wget -q -O- http://ipecho.net/plain; echo}
    ${font sans-serif:normal:size=8}Down: ${downspeed wlp3s0}  ${alignr}Up: ${upspeed wlp3s0} 

    ${font sans-serif:bold:size=10}TOP PROCESSES ${hr 2}
    ${font sans-serif:normal:size=9}Name $alignr PID   CPU%   MEM%${font sans-serif:normal:size=9}
    ${top name 1} $alignr ${top pid 1} ${top cpu 1}% ${top mem 1}%
    ${top name 2} $alignr ${top pid 2} ${top cpu 2}% ${top mem 2}%
    ${top name 3} $alignr ${top pid 3} ${top cpu 3}% ${top mem 3}%
    ${top name 4} $alignr ${top pid 4} ${top cpu 4}% ${top mem 4}%
    ${top name 5} $alignr ${top pid 5} ${top cpu 5}% ${top mem 5}%
    ]];

