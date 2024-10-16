# Linux-Streamer-Mirror-Jetson
Linux software embedded for Jetson Xavier development kit

### Setup guide
Step 1:

	git clone https://github.com/jetsonhacks/bootFromExternalStorage.git

	cd bootFromExternalStorage

	./get_jetson_files.sh

	
	
	Sửa install_jetson_default_packages.sh để cài đặt cuda,opencv...


Step 2:


	- Đưa jetson vào chế độ Force Recovery : Kết nối typeC => kết nối nguồn => Nhấn giữ cần nút Recovery và nút nguồn cho đến khi jetson khởi động lại 
	
		Kiểm tra bằng lệnh  lsusb nếu hiện dòng Nvidia là ok
		
	- Vào file Linux_for_Tegra/tools/kernel_flash/initrd_flash/nv_enable_remote.sh 
	
	line211:	echo "${cfg_str:1}" > "${cfg}/strings/0x409/configuration"

			+ echo on > /sys/bus/usb/devices/usb2/power/control   ( thêm dòng này vào giữa 2 dòng ban đầu đã có)
		
			echo "${udc_dev}" > UDC
	
	 -  Vào Linux_for_Tegra/bootloader/t186ref/BCT/tegra234-mb2-bct-misc-p3767-0000.dts
	  
	  	- cvb_eeprom_read_size = <0x100> (bỏ)
		+ cvb_eeprom_read_size = <0x0>   (thay bằng dòng này)	
		
		
Step 3:

	./flash_jetson_external_storage.sh