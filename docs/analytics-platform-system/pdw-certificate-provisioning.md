---
title: Provisionamento de certificado PDW - Analytics Platform System | Microsoft Docs
description: A página de provisionamento de certificado PDW do Analytics Platform System Configuration Manager importa ou remove o certificado usado pela região PDW.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea52c615f4629b579f5f239513c84d851de9e487
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>Provisionamento de certificado PDW - Analytics Platform System
O **provisionamento de certificados do PDW** página do sistema de plataforma de análise de **do Configuration Manager** importa ou remove o certificado usado pela região PDW. Usando o, um certificado para criptografar conexões pode ajudar a comunicação segura para o nó de controle por meio de clientes do SQL Server, ferramentas que usam os drivers do SQL Server PDW o [Console de administração](monitor-the-appliance-by-using-the-admin-console.md), e carrega os serviços de integração.  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de instalar o certificado, faça o seguinte:  
  
1.  Obtenha um certificado de seguro. Se você precisar de mais informações sobre como obter um certificado de seguro, entre em contato com o Microsoft Support.  
  
2.  Salve o certificado para o nó de controle em um arquivo PFX protegido por senha.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Por motivos de segurança, obter um certificado confiável  
SQL Server PDW oferece suporte ao uso de um certificado para criptografar conexões ao nó de controle; incluindo conexões com o **Console de administração**.  
  
Por padrão, o **Console de administração** inclui um certificado autoassinado que fornece privacidade, mas não a autenticação do servidor. Isso pode deixar as comunicações vulnerável a um ataque man-in-the-middle. Quando um usuário se conecta ao Console do administrador usando o certificado autoassinado, Internet Explorer retorna o erro: "Há um problema com o certificado de segurança do site".  
  
Embora a conexão por meio do certificado autoassinado criptografa os dados em trânsito entre o cliente e o servidor, a conexão é ainda ameaçado por invasores.  
  
> [!WARNING]  
> Os administradores do dispositivo imediatamente devem adquirir um certificado que se conecte a uma autoridade de certificação confiável reconhecida por clientes, para ter uma conexão segura e remover o erro que os relatórios do Internet Explorer.  
  
O caminho de certificação deve conter o nome de domínio totalmente qualificado que mapeia para o nó de controle de endereço IP do Cluster (recomendado) ou o nome que os usuários digitam em seus barras de endereço do navegador para acessar o **Console de administração**.  
  
Use o Analytics Platform System**do Configuration Manager** para adicionar ou remover o certificado confiável. Diretamente usando a ferramenta de configuração de certificado Microsoft Windows HTTP Services (**winHttpCertCfg.exe**) gerenciar o certificado não tem suporte.  
  
## <a name="import-or-remove-the-certificate"></a>Importar ou remover o certificado  
As instruções a seguir mostram como importar ou remover o certificado do dispositivo.  
  
### <a name="to-import-the-certificate"></a>Para importar o certificado  
  
1.  Inicie o **do Configuration Manager**. Para obter mais informações, consulte [iniciar o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do **do Configuration Manager**, expanda **topologia de depósito de dados paralela**e, em seguida, clique em **certificados**.  
  
3.  Selecione **importar um certificado e configurar o dispositivo para usá-lo**e, em seguida, clique em **procurar** navegar e selecionar o arquivo de certificado.  
  
4.  Digite a senha do certificado no **senha** campo.  
  
5.  Clique em **aplicar** para configurar o certificado para o dispositivo.  
  
SQL Server PDW não irá criptografar a conexão atual usando o certificado importado, mas usar o certificado para conexões novas.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>Para remover o certificado importado anteriormente  
  
1.  Inicie o **do Configuration Manager**. Para obter mais informações, consulte [iniciar o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do **do Configuration Manager**, expanda **topologia de depósito de dados paralela**e, em seguida, clique em **certificados**.  
  
3.  Selecione **remover qualquer certificado configurado no dispositivo de**.  
  
4.  Clique em **aplicar** ao remover o certificado importado anteriormente do dispositivo.  
  
SQL Server PDW continuará criptografar conexões atuais, mas não usará o remover o certificado para conexões novas.  
  
![DWConfig Appliance PDW Certificate](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
