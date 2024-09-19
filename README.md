### Resource: https://www.youtube.com/playlist?list=PL55uMtDpag8q3bw30ZSUT2L_nv3HQHomc

### To view result after exposing service
    way-1 : minikube service recreate-type-service
    way-2 : <minikube_ip>:<nodeport_port> 

    to view minikube ip cmd from terminal : minikube ip

## Remember : To view output from UI using minikubeIP:NodePort, try opening it in incognito every time for viewing better output

### Recreate-Strategy

    firstly the image tag is blue

    then change the image tag from blue to orange

    before changing and apply the recreate.yaml
    run : kubectl get pods --watch so that we can see the pod states

    after changing yaml run kubctl apply -f recreate.yaml
    then look in the browser again, there we will see some downtime and after that orange bar will be visible


### RollingUpdate-Strategy

    we don't need to add strategy type rolling update in the yaml. but here i have added it though.
    so same process e image change kore orange/red/green kore abr file save kore apply kori.
    sathe od watch kori and UI ta follow kori



### Blue-Green Strategy

    first e blue.yaml diye deployment and service create korbo,
    then green.yaml diye deployment and service create krbo.

    ekhane blue pods gula update hobe green pods diye
    so jehetu blue er pod 2 ta tai green er pod 2 ta diye update korbo.
    that means amader kache akhn 4 ta pod ase.
    so kono pod delete hbe na. just service traffic blue pod point er jaigai
    green pod point korbe. r jodi kono issue hoi tahole abr blue pod point korbe. etai blue green deployment strategy

    so, tai blue.yaml er service section e green pod gula point kore deyar jnno amra just label and selector section e
    green pod gular label and selector add kore dibo. and save kore abr apply -f bluue.yaml marbo.

    => akhn output dekhar jnno new incognito browser e oi IP:PORT hit krbo
    second way hocche minikube dashboard e service ta check korbo.
    akhn dekhbo je service traffic green pod gula point kore ase



### Canary Strategy

    => example of canary bird and mining gold.
    some percentage of people go to mine with canary bird to inhale gas while mining. if everything okay.
    other percentage of people or whole people will go to mine gold. it is a progressive process.


    => akhn chinta kori amader 3 ta pod ase akta deployment er replica set er moddhe
    so, amra cacchi 30% of the pod new akta pod diye replace korar try korbo kichu change kore
    ekhane pod ase 3 ta so, per pod er % holo 100/3 = 33%
    so 30% means amra 1 ta pod e change kore oitake previous pod diye replace korbo.
    jodi everything okay hoy tahole baki pod gula keo ei percentage akare replace korte thakbo 

    so amader blue replicas ase 3 ta, akhon 30% pod change korte hole 
    blue.yaml e replica 3 er jaigai 2 kore dibo
    and akta red.yaml create kore oitate replica 1 kore dibo and labels gula blue er label diye replace kore dibo
    red.yaml er moddhe. then blue er akta replica delete kore dibo.


    eta akta manual process jodio evabe production e kaj kora thik na.
    will try how automatically we can do it ?
    ans : we can do canary by setting percentage by using ISTIO
