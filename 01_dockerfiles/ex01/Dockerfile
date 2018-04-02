FROM 	debian

RUN 	apt-get update && apt-get install -yqq \
		wget
		

RUN 	adduser --disabled-password --gecos "teamspeak" teamspeak

USER 	teamspeak

RUN 	cd /home/teamspeak && \
		wget http://dl.4players.de/ts/releases/3.0.11.2/teamspeak3-server_linux-amd64-3.0.11.2.tar.gz && \
		tar -zxvf teamspeak3-server_linux-amd64-3.0.11.2.tar.gz && \
		rm teamspeak3-server_linux-amd64-3.0.11.2.tar.gz

EXPOSE 	9987/udp
EXPOSE 	30033
EXPOSE 	10011

CMD  	["/home/teamspeak/teamspeak3-server_linux-amd64/ts3server_minimal_runscript.sh"]
