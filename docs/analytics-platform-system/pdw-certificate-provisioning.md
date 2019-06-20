---
title: Provisionamento de certificado do PDW - Analytics Platform System | Microsoft Docs
description: A página de provisionamento de certificado PDW do Analytics Platform System Configuration Manager importa ou remove o certificado usado pela região PDW.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: af6d4df964820ced9f4d79b67859e010a895bc29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639900"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>Provisionamento de certificado do PDW - Analytics Platform System
O **provisionamento de certificado do PDW** página do Analytics Platform System **Configuration Manager** importa ou remove o certificado usado pela região PDW. Usando o, um certificado para criptografar conexões pode ajudar a comunicação segura para o nó de controle por meio de clientes do SQL Server, as ferramentas que usam os drivers do SQL Server PDW, o [Console de administração](monitor-the-appliance-by-using-the-admin-console.md), e carrega os serviços de integração.  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de instalar o certificado, faça o seguinte:  
  
1.  Obter um certificado seguro. Se você precisar de mais informações sobre como obter um certificado seguro, entre em contato com o Microsoft Support.  
  
2.  Salve o certificado para o nó de controle em um arquivo PFX protegido por senha.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Por motivos de segurança, obter um certificado confiável  
Usando um certificado para criptografar conexões ao nó de controle; dá suporte ao SQL Server PDW incluindo conexões com o **Console de administração**.  
  
Por padrão, o **Console de administração** inclui um certificado autoassinado que fornece privacidade, mas não a autenticação do servidor. Isso pode deixar as comunicações vulnerável a um ataque man-in-the-middle. Quando um usuário se conecta ao Console do administrador usando o certificado autoassinado, o Internet Explorer retornará o erro: "Há um problema com o certificado de segurança do site".  
  
Embora a conexão por meio de um certificado autoassinado criptografa os dados em trânsito entre o cliente e o servidor, a conexão é ainda ameaçado por invasores.  
  
> [!WARNING]  
> Os administradores do dispositivo imediatamente devem adquirir um certificado que se encadeie a uma autoridade de certificação confiável reconhecido pelos clientes, para ter uma conexão segura e remover o erro que informa do Internet Explorer.  
  
O caminho de certificação deve conter o nome de domínio totalmente qualificado que é mapeado para o nó de controle de endereço IP do Cluster (recomendado) ou o nome que os usuários digitam em suas barras de endereço do navegador para acessar o **Console de administração**.  
  
Use o Analytics Platform System**Configuration Manager** para adicionar ou remover o certificado confiável. Diretamente usando a ferramenta de configuração de certificado Microsoft Windows HTTP Services (**winHttpCertCfg.exe**) gerenciar o certificado não tem suporte.  
  
## <a name="import-or-remove-the-certificate"></a>Importar ou remover o certificado  
As instruções a seguir mostram como importar ou remover o certificado do dispositivo.

> [!WARNING]
> Para renovar um certificado expirado, você deve remover o certificado existente antes de importar um novo.
  
### <a name="to-import-the-certificate"></a>Para importar o certificado  
  
1.  Inicie o **Configuration Manager**. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do **Configuration Manager**, expanda **topologia de depósito de dados paralela**e, em seguida, clique em **certificados**.  
  
3.  Selecione **importar um certificado e configure o dispositivo para usá-lo**e, em seguida, clique em **procurar** para procurar e selecione o arquivo de certificado.  
  
4.  Insira a senha do certificado na **senha** campo.  
  
5.  Clique em **aplicar** para configurar o certificado para o dispositivo.  
  
SQL Server PDW não irá criptografar a conexão atual, usando o certificado importado, mas usará o certificado para novas conexões.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>Para remover o certificado importado anteriormente  
  
1.  Inicie o **Configuration Manager**. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do **Configuration Manager**, expanda **topologia de depósito de dados paralela**e, em seguida, clique em **certificados**.  
  
3.  Selecione **remover qualquer certificado provisionado no dispositivo**.  
  
4.  Clique em **aplicar** ao remover o certificado importado anteriormente do dispositivo.  
  
SQL Server PDW continuará criptografar conexões atuais, mas não usará o remover o certificado para novas conexões.  
  
![DWConfig Appliance PDW Certificate](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
