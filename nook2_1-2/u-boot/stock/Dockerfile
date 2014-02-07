# BUILD-USING:        docker build -t drewbug/nook2_1-2_u-boot_stock .
# RUN-USING:          docker run -name u-boot drewbug/nook2_1-2_u-boot_stock && docker wait u-boot && docker cp u-boot:/distro/u-boot/u-boot.bin . && docker rm u-boot

FROM          drewbug/nook2_1-2_base
MAINTAINER    Drew Carey Buglione <me@drewb.ug>

WORKDIR       /distro/u-boot

RUN           make omap3621_gossamer_splash_config
CMD           make
