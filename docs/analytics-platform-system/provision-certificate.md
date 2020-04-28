---
title: Provisionamento de certificado
description: Provisionamento de certificado no Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 669e65a7d27b208d861a33618d889707134dfefa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400508"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Provisionamento de certificado no Analytics Platform System
A página de **provisionamento de certificados do PDW** do sistema de plataforma de análise**Configuration Manager** importa ou remove o certificado usado pelo PDW. 

Usando o, um certificado para criptografar conexões pode ajudar a proteger a comunicação com o nó de controle por meio de clientes SQL Server, ferramentas que usam drivers de SQL Server PDW, o [console de administração](monitor-the-appliance-by-using-the-admin-console.md)e cargas de Integration Services. 
  
## <a name="prerequisites"></a>Pré-requisitos  
Antes de instalar o certificado, faça o seguinte:  
  
1.  Obtenha um certificado seguro. Se você precisar de mais informações sobre como obter um certificado seguro, entre em contato com Suporte da Microsoft.  
  
2.  Salve o certificado no nó de controle em um arquivo PFX protegido por senha.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Por motivos de segurança, obtenha um certificado confiável  
O SQL Server PDW dá suporte ao uso de um certificado para criptografar conexões com o nó de controle; incluindo conexões ao **console de administração**.  
  
Por padrão, o **console de administração** do inclui um certificado autoassinado que fornece privacidade, mas não autenticação de servidor. Isso pode deixar as comunicações vulneráveis a um ataque man-in-the-Middle. Quando um usuário se conecta ao console de administração usando o certificado autoassinado, o Internet Explorer retorna o erro: "há um problema com o certificado de segurança deste site".  
  
Embora a conexão por meio do certificado autoassinado criptografe dados em trânsito entre o cliente e o servidor, a conexão ainda está em risco de invasores.  
  
> [!WARNING]  
> Os administradores de dispositivo devem adquirir imediatamente um certificado que se encadeia com uma autoridade de certificação confiável reconhecida pelos clientes, a fim de ter uma conexão segura e remover o erro que o Internet Explorer relata.  
  
O caminho de certificação deve conter o nome de domínio totalmente qualificado que mapeia para o endereço IP do cluster do nó de controle (recomendado) ou o nome que os usuários digitam em suas barras de endereço do navegador para acessar o **console de administração**.  
  
Use o**Configuration Manager** do sistema de plataforma de análise para adicionar ou remover o certificado confiável. Não há suporte para o uso direto da ferramenta de configuração de certificado do Microsoft Windows HTTP Services (**winHttpCertCfg. exe**) para gerenciar o certificado.  
  
## <a name="import-or-remove-the-certificate"></a>Importar ou remover o certificado  
As instruções a seguir mostram como importar ou remover o certificado do dispositivo.  
  
### <a name="to-import-the-certificate"></a>Para importar o certificado  
  
1.  Inicie o **Configuration Manager**.  
Para obter mais informações, consulte [iniciar o Configuration Manager &#40;&#41;do sistema de plataforma de análise ](launch-the-configuration-manager.md).  

2.  No painel esquerdo da **Configuration Manager**, expanda **data warehouse topologia paralela**e clique em **certificados**.  
  
3.  Selecione **importar um certificado e configure o dispositivo para usá-lo**e clique em **procurar** para procurar e selecionar o arquivo de certificado.  
  
4.  Insira a senha para o certificado no campo **senha** .  
  
5.  Clique em **aplicar** para configurar o certificado para o dispositivo.  
  
SQL Server PDW não criptografará a conexão atual usando o certificado importado, mas usará o certificado para novas conexões.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>Para remover o certificado importado anteriormente  
  
1.  Inicie o **Configuration Manager**. 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  No painel esquerdo da **Configuration Manager**, expanda **data warehouse topologia paralela**e clique em **certificados**.  
  
3.  Selecione **remover qualquer certificado provisionado no dispositivo**.  
  
4.  Clique em **aplicar** para remover o certificado importado anteriormente do dispositivo.  
  
SQL Server PDW continuará a criptografar as conexões atuais, mas não usará o certificado removido para novas conexões.  
  
![Certificado PDW do dispositivo DWConfig](media/dwconfig-appl-pdw-cert.png "Certificado de PDW do dispositivo DWConfig")  
  
## <a name="see-also"></a>Consulte Também  
[Inicie o Configuration Manager &#40;o sistema de plataforma de análise&#41;](launch-the-configuration-manager.md)  
