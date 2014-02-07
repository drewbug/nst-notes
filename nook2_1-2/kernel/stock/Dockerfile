# BUILD-USING:        docker build -t drewbug/nook2_1-2_kernel_stock .
# RUN-USING:          docker run -name kernel drewbug/nook2_1-2_kernel_stock && docker wait kernel && docker cp kernel:/distro/kernel/arch/arm/boot/uImage . && docker rm kernel

FROM          drewbug/nook2_1-2_base
MAINTAINER    Drew Carey Buglione <me@drewb.ug>

WORKDIR       /distro/kernel

RUN           make omap3621_gossamer_evt1c_defconfig
CMD           make uImage
