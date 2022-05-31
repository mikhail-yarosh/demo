FROM ubuntu:bionic

# Build the App
RUN apt update && apt upgrade -y && apt install make gcc git libssl1.0-dev zlib1g-dev dpkg-dev mini-dinstall -y
RUN mkdir -p /app && cd app && git clone https://github.com/peervpn/peervpn && cd peervpn && make

# Create .deb package
## Get the app version and create a deb package.
WORKDIR /pkg
RUN export MAJOR_VERSION=`grep -r "PEERVPN_VERSION_MAJOR" /app/peervpn/globals.ic | awk '{print $3}'` && export MINOR_VERSION=`grep -r "PEERVPN_VERSION_MINOR" /app/peervpn/globals.ic | awk '{print $3}'` && \
    mkdir -p peervpn_$MAJOR_VERSION.$MINOR_VERSION-0_amd64/usr/local/bin/ && cp /app/peervpn/peervpn peervpn_$MAJOR_VERSION.$MINOR_VERSION-0_amd64/usr/local/bin/ && \
    mkdir -p peervpn_$MAJOR_VERSION.$MINOR_VERSION-0_amd64/DEBIAN && \
    echo "Package: peervpn \nVersion: $MAJOR_VERSION.$MINOR_VERSION \nArchitecture: amd64 \nMaintainer: WhoKnows... \nDescription: PeerVPN https://github.com/peervpn/peervpn. \n" > peervpn_$MAJOR_VERSION.$MINOR_VERSION-0_amd64/DEBIAN/control && \
    echo "" > peervpn_$MAJOR_VERSION.$MINOR_VERSION-0_amd64/DEBIAN/changelog && \
    dpkg-deb --build --root-owner-group peervpn_$MAJOR_VERSION.$MINOR_VERSION-0_amd64
