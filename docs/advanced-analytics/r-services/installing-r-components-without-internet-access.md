---
title: "Instala&#231;&#227;o de Componentes de R sem Acesso &#224; Internet | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 21
---
# Instala&#231;&#227;o de Componentes de R sem Acesso &#224; Internet
  A instalação dos componentes de R usados pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requer uma conexão com a Internet para acessar arquivos que são fornecidos no Centro de Download da Microsoft ou em outro site confiável. No entanto, você pode instalar esses componentes em um servidor sem acesso à Internet fazendo cópias locais, conforme descrito neste tópico.  
  
  > [!TIP]
  > 
  > Para obter um passo a passo detalhado do processo de instalação offline, confira este blog da [Equipe de Consultoria para Clientes do SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)
  
## <a name="installation-on-computers-with-no-internet-access"></a>Instalação em Computadores sem Acesso à Internet  
 Se você estiver executando uma instalação offline, o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não poderá acessar os links para instalar os componentes necessários do R. Para evitar esse problema, baixe uma cópia dos instaladores localmente e conclua a instalação, conforme descrito aqui.
 
 Observe que há dois instaladores para os componentes do R: um para o Microsoft R Open e outro para o Microsoft R Server. Baixe e instale os dois para usar o SQL Server R Services. O assistente de instalação do SQL Server assegurará que eles sejam instalados na ordem correta.


Versão  |Link de download  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab: ](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  

  
**Como atualizar os componentes do R em uma instalação offline**     

1. Use os links listados acima para baixar a versão apropriada.
2. Copie os arquivos CAB para uma pasta no computador na qual você instalará a atualização.
3. Ao executar o assistente de instalação do SQL Server, clique em **Aceitar** na página de licenciamento do Microsoft R.  Será exibida uma caixa de diálogo que lista os links para os downloads. Insira o caminho para a localização dos arquivos que você baixou. 
4. Clique em **Avançar** para indicar que os componentes estão disponíveis e conclua o assistente de instalação do SQL Server.
5. Opcionalmente, você também pode baixar o código-fonte arquivado para os componentes de software livre. Para obter mais informações, consulte [Configurar o SQL Server R Services (no Banco de Dados)](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).


> [!IMPORTANT] Se você baixar os arquivos .cab como parte da instalação do SQL Server em um computador com acesso à Internet, o assistente de instalação detectará o idioma local e alterará o idioma do instalador automaticamente. 
> 
> No entanto, se você estiver instalando uma das versões localizadas do SQL Server em um computador sem acesso à Internet e baixar os instaladores do R em um compartilhamento local, será necessário editar o nome dos arquivos baixados manualmente e inserir o identificador de idioma correto para o idioma que está sendo instalado. 
> 
> Por exemplo, se você estiver instalando a versão japonesa do SQL Server, altere o nome do arquivo de SRS_8.0.3.0_1033.cab para SRS_8.0.3.0_1041.cab.    
 
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Solução de problemas da configuração do R Services](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  