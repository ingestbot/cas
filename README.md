
# Content Aquisiton System (CAS)

Content Aquisition System (CAS) is a construction of various softwares which allow for the safe and private transfer of data across the internet.

This is a work in progress. Although this architecture is functioning within known environments, there are many details to refine to allow for ease of accessibility for a larger audience.

The motiviation for starting this project is to encourage a maximum of privacy and security; ease of assembly and maintenance; and ultimately increase options in media accessibility.

Please use the Discussions section of this repository (horizontal navigation) to ask questions, offer suggestions, praise, and criticism. As this project becomes more technically
focused, the Issues section will be used for pull requests, bugs, etc. 

## Requirements

* Patience and Curiosity
* Intermediate Networking (tcp/ip, VPN)
* Intermediate Linux, Containers (Docker), VMs (VirtualBox, KVM)
* General Torrent (download clients, magnet files, etc)
* General *Arr (Radarr, Sonarr, etc.) https://wiki.servarr.com/
* Seedbox (optional, see reddit.com/r/seedboxes)

## Diagram / Overview 

The topics which follow are based on [this diagram](images/cas_arch.png).

## Network Considerations

Most components shown in the diagram are functioning on separate networks. While this isn't necessary for all configurations, it's encouraged in offering increased privacy and 
security.

## Seedbox

This project encourages the use of a seedbox as a means of torrenting. This extends the activity of collecting torrents to a domain outside of a local network. Access to the
seedbox should make use of a VPN, including ssh and transfer of data. 

## Virtual Machine (VM)

The Virtual Machine (VM) show here involves the use of the [Gluetun VPN Client](https://github.com/qdm12/gluetun). Use of [Gluetun VPN Randomizer](https://github.com/ingestbot/randomizer) 
is encouraged to maximize privacy.

Data from the seedbox is transferred via [Syncthing](https://syncthing.net) through the VPN tunneling through a [SOCKS5 proxy](https://docs.syncthing.net/users/proxying.html).

Once the data has been fully transferred, the *Arr components then process, organize, and make items available for transfer to the Media Center.

## Arr Components

See [/arr](/arr)

## Media Center

The Media Center shown in this project is currently [Emby](https://emby.media/), but could involve Kodi, Plex, Jellyfin, etc. The data is simply transferred from the 
VM to a local library that the media server software is aware of.

## Control Clients

Control Clients shown here are simply laptops, desktops, and phones with web browsers connecting to the *Arr components making requests.

Important to note that clients with ssh should connect to the seedbox via the SOCKS5 proxy. Here are a couple of examples to accomplish this:

`ssh -i id_ed25519.seedbox -o "ProxyCommand=nc -X 5 -x socks:1080 %h %p" mynewusername@seedbox`

```
~/.ssh/config:

Host myseedbox
 ProxyCommand nc -X 5 -x socks:1080 %h %p
 HostName emmas.seedbox.me
 User emmastone
 IdentityFile ~/.ssh/id_ed25519.seedbox
```

## Viewing 

The viewing component will be unique to your environement and the only requirement is that it can access the Media Center for the playing of content.

### Roku

A Roku device is shown here on a separate network. 

### Projector

A projector is used to display content via HDMI connection to the Roku. 

