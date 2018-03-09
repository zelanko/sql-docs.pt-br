---
title: Recursos internacionais do JDBC Driver | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
caps.latest.revision: "40"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f323a5728aa9f63ba5283a34694c1e00baa0bb91
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="international-features-of-the-jdbc-driver"></a>Recursos internacionais do JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Os recursos de internacionalização do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] incluem o seguinte:  
  
-   Suporte para uma experiência totalmente localizada nos mesmos idiomas como[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Suporte para as conversões da linguagem Java para confidenciais [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dados  
  
-   Suporte a idiomas internacionais, independentemente do sistema operacional  
  
-   Suporte para nomes de domínio internacionais (começando com o Microsoft JDBC Driver 6.0 para o SQL Server)  
  
## <a name="handling-of-character-data"></a>Manipulação de dados de caractere  
 Dados de caractere no Java são tratados como Unicode por padrão. o Java **cadeia de caracteres** objeto representa dados de caractere Unicode. No driver JDBC, a única exceção a esta regra são os métodos getter e setter de fluxo ASCII que são casos especiais porque usam fluxos de byte com a pressuposição implícita de páginas de código simples e conhecidas (ASCII).  
  
 Além disso, o driver JDBC fornece o **sendStringParametersAsUnicode** propriedade de cadeia de caracteres de conexão. Essa propriedade pode ser usada para especificar que os parâmetros preparados para dados de caracteres sejam enviados como ASCII ou conjunto de caracteres multibyte (MBCS) em vez de Unicode. Para obter mais informações sobre o **sendStringParametersAsUnicode** propriedade de cadeia de caracteres de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
### <a name="driver-incoming-conversions"></a>Conversões de entrada de driver  
 Os dados de texto em Unicode que vêm do servidor não precisam ser convertidos. Eles são passados diretamente como Unicode. Os dados não Unicode que vêm do servidor são convertidos da página de código para os dados, no nível de coluna ou de banco de dados, para Unicode. O driver JDBC usa as rotinas de conversão da Máquina Virtual Java (JVM) para realizar estas conversões. Estas conversões são executadas em todos os métodos getter de fluxo de caracteres e cadeia de caracteres com tipo.  
  
 Se o JVM não tiver o suporte apropriado à página de código para os dados do banco de dados, o driver JDBC lançará uma exceção de "página de código de XXX sem suporte pelo ambiente Java". Para resolver este problema, instale o suporte completo de caractere internacional exigido para essa JVM. Para obter um exemplo, consulte a documentação de Codificações com Suporte no site da Sun Microsystems.  
  
### <a name="driver-outgoing-conversions"></a>Conversões de saída de driver  
 Os dados de caractere que vão do driver para o servidor podem ser ASCII ou Unicode. Por exemplo, os novo caracteres nacionais métodos do JDBC 4.0, como métodos setNString, setNCharacterStream e setNClob de [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes, sempre enviam os valores de parâmetro para o servidor em Unicode.  
  
 Por outro lado, os métodos da API de caracteres não nacionais, como métodos setString, setCharacterStream e setClob de [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes enviar seus valores para o servidor em Unicode somente quando o **sendStringParametersAsUnicode** propriedade é definida como "true", que é o valor padrão.  
  
## <a name="non-unicode-parameters"></a>Parâmetros não Unicode  
 Para obter ótimo desempenho com **CHAR**, **VARCHAR** ou **LONGVARCHAR** tipo de parâmetros não Unicode, defina o **sendStringParametersAsUnicode** a propriedade como "false" de cadeia de caracteres de conexão e usar os métodos de caractere não nacional.  
  
## <a name="formatting-issues"></a>Problemas de formatação  
 Para data, hora e moedas, toda a formatação com dados localizados é realizada no nível da linguagem Java usando o objeto de localidade; e os vários métodos de formatação para **data**, **calendário**, e **número** tipos de dados. Em casos raros em que o JDBC Driver precisar passar dados que fazem distinção de localidade em um formato localizado, o formatador correto é usado com a localidade padrão da JVM.  
  
## <a name="collation-support"></a>Suporte a agrupamentos  
 O JDBC Driver 3.0 oferece suporte a todos os agrupamentos com suporte [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]e os novos agrupamentos ou as novas versões do Windows, nomes de agrupamento introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
 Para obter mais informações sobre os agrupamentos, consulte [Collation and Unicode Support](http://go.microsoft.com/fwlink/?LinkId=131366) e [nome de agrupamento do Windows (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=131367) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="using-international-domain-names-idn"></a>Usando nomes de domínio internacionais (IDN)  
 O JDBC Driver 6.0 para SQL Server oferece suporte ao uso de nomes de domínio internacionalizados (IDNs) e pode converter um serverName Unicode para compatível com codificação ASCII (Punycode) quando solicitado durante uma conexão.  Se os IDNs forem armazenados no sistema de nome de domínio (DNS) como cadeias de caracteres ASCII no formato Punycode (especificado pela RFC 3490), habilite a conversão do nome do servidor Unicode definindo a propriedade serverNameAsACE como true.  Caso contrário, se o serviço DNS é configurado para permitir o uso de caracteres Unicode, defina a propriedade de serverNameAsACE como falso (padrão).  Para versões mais antigas do driver JDBC, também é possível converter o serverName em Punycode usando [ToAscii do Java](http://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) métodos antes de definir essa propriedade para uma conexão.  
  
> [!NOTE]  
>  A maioria dos softwares de resolvedor escritos para plataformas não Windows baseia-se nos padrões da Internet DSN e, portanto, é mais provável usar o formato Punycode IDNs, enquanto um servidor DNS baseados no Windows em uma rede privada pode ser configurado para permitir o uso de caracteres UTF-8 em uma base por servidor.  Para obter mais detalhes, consulte [suporte a caracteres Unicode](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
