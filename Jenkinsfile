@Library('Libs') __

pipeline {
    agent any   
    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '25'))
    }
    parameters {
        string(name: 'NAME', defaultValue: 'Teschtle Ralf Merznicht', description: 'hier kann Zusatzinfo eingetrgen werden')
        text(name: 'DESC', defaultValue: 'Teschtle Beschreibung Ralf Merznicht', description: 'hier kann Zusatzinfo eingetragen werden')
        booleanParam(name: 'DRY_RUN', defaultValue: true, description: 'Do not execute Sqlserver Procedures')
        choice(name: 'DEVTESTPROD', choices: ['Dev', 'Test', 'Prod'], description: 'Server auswählen (aktuell nur DUMMY Parameter)')        
        choice(name: 'SLEEPSECONDS', choices: ['30', '10', '20', '40', '50', '60', '120', '240'], description: 'Sekunden SLEEP Dauer in der Warteschleife')
        choice(name: 'WAITMINUTES', choices: ['1', '2', '3', '4', '5', '6', '7', '8'], description: 'Wartezeit zwischen den Zeitzonen [nur bei DRY_RUN = TRUE]')
    }   
    stages {
        /*
        stage('WAIT_UNTIL_ASIA_STARTS') {
            environment {
                TIMEZONE = 'Asia'
            }     
                   
            steps {
                    script {
                        try {
                           if (params.DRY_RUN == true) {
                               echo('WaitForNextTimeZone("ASIA")')                    
                           } else {
                               psfunctions.WaitForNextTimeZone()
                           }
                        } catch (e) {
                            echo('WaitForNextTimeZone("ASIA")')
                            throw(e)
                        }
                    }              
            }
        }
        */
        stage('ASISA') {
            parallel {
                stage('STA_TO_PSTA_ISCALA_36') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_PSTA_ISCALA_36()')
                               } else {
                                   psta_iscala_36.function_PSTA_ISCALA_36()
                               }
                            } catch (e) {
                                echo('detected failure: function_PSTA_ISCALA_36()')
                                throw(e)
                            }
                        }
                    }
                }
                stage('STA_TO_PSTA_ISCALA_49') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_PSTA_ISCALA_49()')     
                               } else {
                                   psta_iscala_49.function_PSTA_ISCALA_49()
                               }
                            } catch (e) {
                                echo('detected failure: function_PSTA_ISCALA_49()')
                                throw(e)
                            }
                        }
                    }
                }                      
            }
        }
        /*
        stage('WAIT_UNTIL_EUROPE_STARTS') {
            environment {
                TIMEZONE = 'Europe'
            }   
            steps {
                echo('WaitForNextTimeZone("EUROPE")')
                WaitForNextTimeZone()
            }
        }       
        stage('EUROPE_JH') {
            parallel {
                stage('STA_TO_PSTA_BRAIN') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_BRAIN()')
                               } else {
                                   function_STA_TO_PSTA_BRAIN()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_BRAIN()')
                                // throw(e)
                            }
                        }
                    }
                }
                stage('STA_TO_PSTA_TIS') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_TIS()')
                               } else {
                                   function_STA_TO_PSTA_TIS()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_TIS()')
                                // throw(e)
                            }
                        }
                    }
                }				
                stage('STA_TO_PSTA_SAP_ERP') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_SAP_ERP()')
                               } else {
                                   function_STA_TO_PSTA_SAP_ERP()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_SAP_ERP()')
                                // throw(e)
                            }
                        }
                    }
                }				
                stage('STA_TO_PSTA_SAP_EWM') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_SAP_EWM()')
                               } else {
                                   function_STA_TO_PSTA_SAP_EWM()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_SAP_EWM()')
                                // throw(e)
                            }
                        }
                    }
                }
            }
        }
        stage('EUROPE_ISCALA') {
            parallel {
                stage('STA_TO_PSTA_ISCALA_10') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_ISCALA_10()')
                               } else {
                                   function_STA_TO_PSTA_ISCALA_10()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_ISCALA_10()')
                                // throw(e)
                            }
                        }
                    }
                }				
                stage('STA_TO_PSTA_ISCALA_30') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_ISCALA_30()')
                               } else {
                                   function_STA_TO_PSTA_ISCALA_10()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_ISCALA_30()')
                                // throw(e)
                            }
                        }
                    }
                }	               
            }
        }
        stage('WAIT_UNTIL_SOUTHAMERICA_STARTS') {
            environment {
                TIMEZONE = 'SouthAmerica'
            }   
            steps {
                echo('WaitForNextTimeZone("WAIT_UNTIL_SOUTHAMERICA_STARTS")')
                WaitForNextTimeZone()
            }
        }         
        stage('SAMERICA') {
            parallel {
                stage('STA_TO_PSTA_ISCALA_51') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_ISCALA_51()')
                               } else {
                                   function_STA_TO_PSTA_ISCALA_10()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_ISCALA_51()')
                                // throw(e)
                            }
                        }
                    }
                }
            }           
        }       
        stage('WAIT_UNTIL_NORTHAMERICA_STARTS') {
            environment {
                TIMEZONE = 'NorthAmerica'
            }   
            steps {
                echo('WaitForNextTimeZone("WAIT_UNTIL_NORTHAMERICA_STARTS")')
                WaitForNextTimeZone()
            }
        }      
        stage('NAMERICA') {
            parallel {
                stage('STA_TO_PSTA_ISCALA_70') {
                    steps {
                        script {
                            try {
                               if (params.DRY_RUN == true) {
                                   echo('DRY_RUN = TRUE : function_STA_TO_PSTA_ISCALA_70()')
                               } else {
                                   function_STA_TO_PSTA_ISCALA_10()
                               }
                            } catch (e) {
                                echo('detected failure: function_STA_TO_PSTA_ISCALA_70()')
                                // throw(e)
                            }
                        }
                    }
                }
            }
        }           
        stage('INT_ISCALA') {
            steps {
                script {
                    try {
                        echo('function_INT_ISCALA()')
                    } catch (e) {
                        echo('detected failure: function_INT_ISCALA()')
                        throw(e)
                    }
                }
            }
        }       
        stage('INT_ENTITY') {
            steps {
                script {
                    try {
                        echo('function_INT_ENTITY()')
                    } catch (e) {
                        echo('detected failure: function_INT_ENTITY()')
                        throw(e)
                    }
                }
            }
        }       
        stage('INT_DQ_MONITOR') {
            steps {
                script {
                    try {
                        echo('function_INT_DQ_MONITOR()')
                    } catch (e) {
                        echo('detected failure: function_INT_DQ_MONITOR()')
                        throw(e)
                    }
                }
            }
        }       
        stage('DWH_ENTITY') {
            steps {
                script {
                    try {
                        echo('function_DWH_ENTITY()')
                    } catch (e) {
                        echo('detected failure: function_DWH_ENTITY()')
                        throw(e)
                    }
                }
            }
        }           
        stage('DWH_DQ') {
            steps {
                script {
                    try {
                        echo('function_DWH_DQ()')
                    } catch (e) {
                        echo('detected failure: function_DWH_DQ()')
                        throw(e)
                    }
                }
            }
        }   
        */
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
 
 
def function_INT_ISCALA() {
    stage('INT_ISCALA')
    {
        def INT_ISCALA = [
             sp_t_BOM_DelIns:{build job: 'INT_ISCALA',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT_ISCALA].[sp_t_BOM_DelIns]"]]}
            ,sp_t_LifeCyclePhases_DelIns:{build job: 'INT_ISCALA',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT_ISCALA].[sp_t_LifeCyclePhases_DelIns]"]]}
            ,sp_t_MaterialMaster_DelIns:{build job: 'INT_ISCALA',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT_ISCALA].[sp_t_MaterialMaster_DelIns]"]]}
            ,sp_t_ScalaCompanySegment_DelIns:{build job: 'INT_ISCALA',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT_ISCALA].[sp_t_ScalaCompanySegment_DelIns]"]]}
           
        ]
        parallel INT_ISCALA
    }
}
def function_INT_ENTITY() {
    stage('INT_ENTITY')
    {
        def INT_ENTITY = [
             sp_t_ActiveDirectoryGroupMembers_DelIns:{build job: 'INT_ENTITY',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_ActiveDirectoryGroupMembers_DelIns]"]]}
            ,sp_t_LifeCyclePhases_DelIns:{build job: 'INT_ENTITY',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_MaterialMaster_DelIns]"]]}
            ,sp_t_MaterialOrganisation_DelIns:{build job: 'INT_ENTITY',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_MaterialOrganisation_DelIns]"]]}
            ,sp_t_Organisation_DelIns:{build job: 'INT_ENTITY',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_Organisation_DelIns]"]]}
           
        ]
        parallel INT_ENTITY
    }
}
def function_INT_DQ_MONITOR() {
    stage('INT_DQ_MONITOR')
    {
        def INT_DQ_MONITOR = [
             sp_t_BOM_DelIns_brain:{build job: 'INT_DQ_MONITOR',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_BomUsage_DelIns] Brain"]]}
            ,sp_t_BOM_DelIns_iscala:{build job: 'INT_DQ_MONITOR',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_BomUsage_DelIns] IScala"]]}
            ,sp_t_BOM_DelIns_sap:{build job: 'INT_DQ_MONITOR',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_BomUsage_DelIns] SAP"]]}
            ,sp_t_BOM_DelIns_tis:{build job: 'INT_DQ_MONITOR',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_BomUsage_DelIns] TIS"]]}
            ,sp_t_BOM_DelIns:{build job: 'INT_DQ_MONITOR',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[INT].[sp_t_BomCompare_DelIns]"]]}
 
        ]
        parallel INT_DQ_MONITOR
    }
}
def function_DWH_ENTITY() {
    stage('DWH_ENTITY')
    {
        def DWH_ENTITY = [
             sp_t_MaterialMaster_merge:{build job: 'DWH_ENTITY',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[DWH].[sp_t_MaterialMaster_merge]"]]}
            ,sp_t_MaterialOrganisation_merge:{build job: 'DWH_ENTITY',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[DWH].[sp_t_MaterialOrganisation_merge]"]]}
 
        ]
        parallel DWH_ENTITY
    }
}
def function_DWH_DQ() {
    stage('DWH_DQ')
    {
        def DWH_DQ = [
             sp_t_BomUsage_DelIns:{build job: 'DWH_DQ',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[DWH].[sp_t_BomUsage_DelIns]"]]}
            ,DWH_sp_t_BomCompare_DelIns:{build job: 'DWH_DQ',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[DWH].[sp_t_BomCompare_DelIns]"]]}
 
        ]
        parallel DWH_DQ
    }
}
def function_PSTA_AD() {
    stage('PSTA_AD')
    {
        def PSTA_AD = [
             sp_t_JHDATA_GroupMembers_merge:{build job: 'PSTA_AD_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_AD].[sp_t_JHDATA_GroupMembers_merge]"]]}
 
        ]
        parallel PSTA_AD
    }
}
def function_PSTA_BRAIN() {
    stage('PSTA_BRAIN')
    {
        def PSTA_BRAIN = [
             sp_t_CASPDTA0_BOMPF0WB_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.BOMPF0WB_merge]"]]}
            ,sp_t_CASPDTA0_BOMPF0WD_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.BOMPF0WD_merge]"]]}
            ,sp_t_CASPDTA0_CATLFACL_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.CATLFACL_merge]"]]}
            ,sp_t_CASPDTA0_CATLFAHJ_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.CATLFAHJ_merge]"]]}
            ,sp_t_CASPDTA0_CATPF0CL_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.CATPF0CL_merge]"]]}
            ,sp_t_CASPDTA0_CATPF0HF_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.CATPF0HF_merge]"]]}
            ,sp_t_CASPDTA0_COSPF2L6_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.COSPF2L6_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF01G_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF01G_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF01I_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF01I_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF01K_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF01K_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF01N_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF01N_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF01S_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF01S_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF02V_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF02V_merge]"]]}
            ,sp_t_CASPDTA0_GIDPF300_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.GIDPF300_merge]"]]}
            ,sp_t_CASPDTA0_SCKPF096_DeltaTime:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_CASPDTA0.SCKPF096_DeltaTime]"]]}
            ,sp_t_HHTLIB_W0400P_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_HHTLIB.W0400P_merge]"]]}
            ,sp_t_HHTLIB_W0700P_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_HHTLIB.W0700P_merge]"]]}
            ,sp_t_HHTLIB_W4200P_merge:{build job: 'PSTA_BRAIN_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_BRAIN].[sp_t_HHTLIB.W4200P_merge]"]]}
 
        ]
        parallel PSTA_BRAIN
    }
}
def function_PSTA_EWM() {
    stage('PSTA_EWM')
    {
        def PSTA_EWM = [
             sp_t_SAPAPO_MATKEY_merge:{build job: 'PSTA_EWM_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_EWM].[sp_t_SAPAPO_MATKEY_merge]"]]}
 
        ]
        parallel PSTA_EWM
    }
}
def function_PSTA_ISCALA_10() {
    stage('PSTA_ISCALA_10')
    {
        def PSTA_ISCALA_10 = [
             sp_t_GL0310YY_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_GL0310YY_merge]"]]}
            ,sp_t_MP611000_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_MP611000_merge]"]]}
            ,sp_t_SC011000_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_SC011000_merge]"]]}
            ,sp_t_SC031000_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_SC031000_merge]"]]}
            ,sp_t_SC101000_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_SC101000_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP21000_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_SCP21000_merge]"]]}
            ,sp_t_SCP31000_merge:{build job: 'PSTA_ISCALA_10_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_10].[sp_t_SCP31000_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_10
    }
}
def function_PSTA_ISCALA_30() {
    stage('PSTA_ISCALA_30')
    {
        def PSTA_ISCALA_30 = [
             sp_t_GL0330YY_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_GL0330YY_merge]"]]}
            ,sp_t_MP613000_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_MP613000_merge]"]]}
            ,sp_t_SC013000_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_SC013000_merge]"]]}
            ,sp_t_SC033000_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_SC033000_merge]"]]}
            ,sp_t_SC103000_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_SC103000_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP23000_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_SCP23000_merge]"]]}
            ,sp_t_SCP33000_merge:{build job: 'PSTA_ISCALA_30_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_30].[sp_t_SCP33000_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_30
    }
}
def function_PSTA_ISCALA_40() {
    stage('PSTA_ISCALA_40')
    {
       def PSTA_ISCALA_40 = [
             sp_t_GL0340YY_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_GL0340YY_merge]"]]}
            ,sp_t_MP614000_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_MP614000_merge]"]]}
            ,sp_t_SC014000_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_SC014000_merge]"]]}
            ,sp_t_SC034000_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_SC034000_merge]"]]}
            ,sp_t_SC104000_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_SC104000_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24000_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_SCP24000_merge]"]]}
            ,sp_t_SCP34000_merge:{build job: 'PSTA_ISCALA_40_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_40].[sp_t_SCP34000_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_40
    }
}
def function_PSTA_ISCALA_41() {
    stage('PSTA_ISCALA_41')
    {
        def PSTA_ISCALA_41 = [
             sp_t_GL0341YY_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_GL0341YY_merge]"]]}
            ,sp_t_MP614100_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_MP614100_merge]"]]}
            ,sp_t_SC014100_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_SC014100_merge]"]]}
            ,sp_t_SC034100_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_SC034100_merge]"]]}
            ,sp_t_SC104100_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_SC104100_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24100_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_SCP24100_merge]"]]}
            ,sp_t_SCP34100_merge:{build job: 'PSTA_ISCALA_41_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_41].[sp_t_SCP34100_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_41
    }
}
def function_PSTA_ISCALA_42() {
    stage('PSTA_ISCALA_42')
    {
        def PSTA_ISCALA_42 = [
             sp_t_GL0342YY_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_GL0342YY_merge]"]]}
            ,sp_t_MP614200_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_MP614200_merge]"]]}
            ,sp_t_SC014200_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_SC014200_merge]"]]}
            ,sp_t_SC034200_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_SC034200_merge]"]]}
            ,sp_t_SC104200_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_SC104200_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24200_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_SCP24200_merge]"]]}
            ,sp_t_SCP34200_merge:{build job: 'PSTA_ISCALA_42_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_42].[sp_t_SCP34200_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_42
    }
}
def function_PSTA_ISCALA_43() {
    stage('PSTA_ISCALA_43')
    {
        def PSTA_ISCALA_43 = [
             sp_t_GL0343YY_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_GL0343YY_merge]"]]}
            ,sp_t_MP614300_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_MP614300_merge]"]]}
            ,sp_t_SC014300_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_SC014300_merge]"]]}
            ,sp_t_SC034300_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_SC034300_merge]"]]}
            ,sp_t_SC104300_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_SC104300_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24300_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_SCP24300_merge]"]]}
            ,sp_t_SCP34300_merge:{build job: 'PSTA_ISCALA_43_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_43].[sp_t_SCP34300_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_43
    }
}
def function_PSTA_ISCALA_45() {
    stage('PSTA_ISCALA_45')
    {
        def PSTA_ISCALA_45 = [
             sp_t_GL0345YY_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_GL0345YY_merge]"]]}
            ,sp_t_MP614500_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_MP614500_merge]"]]}
            ,sp_t_SC014500_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_SC014500_merge]"]]}
            ,sp_t_SC034500_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_SC034500_merge]"]]}
            ,sp_t_SC104500_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_SC104500_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24500_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_SCP24500_merge]"]]}
            ,sp_t_SCP34500_merge:{build job: 'PSTA_ISCALA_45_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_45].[sp_t_SCP34500_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_45
    }
}
def function_PSTA_ISCALA_46() {
    stage('PSTA_ISCALA_46')
    {
       def PSTA_ISCALA_46 = [
             sp_t_GL0346YY_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_GL0346YY_merge]"]]}
            ,sp_t_MP614600_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_MP614600_merge]"]]}
            ,sp_t_SC014600_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_SC014600_merge]"]]}
            ,sp_t_SC034600_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_SC034600_merge]"]]}
            ,sp_t_SC104600_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_SC104600_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24600_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_SCP24600_merge]"]]}
            ,sp_t_SCP34600_merge:{build job: 'PSTA_ISCALA_46_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_46].[sp_t_SCP34600_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_46
    }
}
def function_PSTA_ISCALA_47() {
    stage('PSTA_ISCALA_47')
    {
        def PSTA_ISCALA_47 = [
             sp_t_GL0347YY_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_GL0347YY_merge]"]]}
            ,sp_t_MP614700_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_MP614700_merge]"]]}
            ,sp_t_SC014700_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_SC014700_merge]"]]}
            ,sp_t_SC034700_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_SC034700_merge]"]]}
            ,sp_t_SC104700_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_SC104700_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24700_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_SCP24700_merge]"]]}
            ,sp_t_SCP34700_merge:{build job: 'PSTA_ISCALA_47_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_47].[sp_t_SCP34700_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_47
    }
}
def function_PSTA_ISCALA_48() {
    stage('PSTA_ISCALA_48')
    {
        def PSTA_ISCALA_48 = [
             sp_t_GL0348YY_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_GL0348YY_merge]"]]}
            ,sp_t_MP614800_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_MP614800_merge]"]]}
            ,sp_t_SC014800_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_SC014800_merge]"]]}
            ,sp_t_SC034800_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_SC034800_merge]"]]}
            ,sp_t_SC104800_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_SC104800_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP24800_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_SCP24800_merge]"]]}
            ,sp_t_SCP34800_merge:{build job: 'PSTA_ISCALA_48_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_48].[sp_t_SCP34800_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_48
    }
}
def function_PSTA_ISCALA_50() {
    stage('PSTA_ISCALA_50')
    {
        def PSTA_ISCALA_50 = [
             sp_t_GL0350YY_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_GL0350YY_merge]"]]}
            ,sp_t_MP615000_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_MP615000_merge]"]]}
            ,sp_t_SC015000_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_SC015000_merge]"]]}
            ,sp_t_SC035000_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_SC035000_merge]"]]}
            ,sp_t_SC105000_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_SC105000_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP25000_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_SCP25000_merge]"]]}
            ,sp_t_SCP35000_merge:{build job: 'PSTA_ISCALA_50_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_50].[sp_t_SCP35000_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_50
    }
}
def function_PSTA_ISCALA_51() {
    stage('PSTA_ISCALA_51')
    {
        def PSTA_ISCALA_51 = [
             sp_t_GL0351YY_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_GL0351YY_merge]"]]}
            ,sp_t_MP615100_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_MP615100_merge]"]]}
            ,sp_t_SC015100_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_SC015100_merge]"]]}
            ,sp_t_SC035100_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_SC035100_merge]"]]}
            ,sp_t_SC105100_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_SC105100_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP25100_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_SCP25100_merge]"]]}
            ,sp_t_SCP35100_merge:{build job: 'PSTA_ISCALA_51_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_51].[sp_t_SCP35100_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_51
    }
}
def function_PSTA_ISCALA_55() {
    stage('PSTA_ISCALA_55')
    {
        def PSTA_ISCALA_55 = [
             sp_t_GL0355YY_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_GL0355YY_merge]"]]}
            ,sp_t_MP615500_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_MP615500_merge]"]]}
            ,sp_t_SC015500_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_SC015500_merge]"]]}
            ,sp_t_SC035500_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_SC035500_merge]"]]}
            ,sp_t_SC105500_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_SC105500_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP25500_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_SCP25500_merge]"]]}
            ,sp_t_SCP35500_merge:{build job: 'PSTA_ISCALA_55_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_55].[sp_t_SCP35500_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_55
    }
}
def function_PSTA_ISCALA_58() {
    stage('PSTA_ISCALA_58')
    {
       def PSTA_ISCALA_58 = [
             sp_t_GL0358YY_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_GL0358YY_merge]"]]}
            ,sp_t_MP615800_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_MP615800_merge]"]]}
            ,sp_t_SC015800_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_SC015800_merge]"]]}
            ,sp_t_SC035800_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_SC035800_merge]"]]}
            ,sp_t_SC105800_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_SC105800_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP25800_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_SCP25800_merge]"]]}
            ,sp_t_SCP35800_merge:{build job: 'PSTA_ISCALA_58_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_58].[sp_t_SCP35800_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_58
    }
}
def function_PSTA_ISCALA_60() {
    stage('PSTA_ISCALA_60')
    {
        def PSTA_ISCALA_60 = [
             sp_t_GL0360YY_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_GL0360YY_merge]"]]}
            ,sp_t_MP616000_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_MP616000_merge]"]]}
            ,sp_t_SC016000_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_SC016000_merge]"]]}
            ,sp_t_SC036000_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_SC036000_merge]"]]}
            ,sp_t_SC106000_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_SC106000_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP26000_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_SCP26000_merge]"]]}
            ,sp_t_SCP36000_merge:{build job: 'PSTA_ISCALA_60_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_60].[sp_t_SCP36000_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_60
    }
}
def function_PSTA_ISCALA_70() {
    stage('PSTA_ISCALA_70')
    {
        def PSTA_ISCALA_70 = [
             sp_t_GL0370YY_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_GL0370YY_merge]"]]}
            ,sp_t_MP617000_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_MP617000_merge]"]]}
            ,sp_t_SC017000_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_SC017000_merge]"]]}
            ,sp_t_SC037000_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_SC037000_merge]"]]}
            ,sp_t_SC107000_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_SC107000_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP27000_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_SCP27000_merge]"]]}
            ,sp_t_SCP37000_merge:{build job: 'PSTA_ISCALA_70_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_70].[sp_t_SCP37000_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_70
    }
}
def function_PSTA_ISCALA_71() {
    stage('PSTA_ISCALA_71')
    {
        def PSTA_ISCALA_71 = [
             sp_t_GL0371YY_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_GL0371YY_merge]"]]}
            ,sp_t_MP617100_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_MP617100_merge]"]]}
            ,sp_t_SC017100_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_SC017100_merge]"]]}
            ,sp_t_SC037100_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_SC037100_merge]"]]}
            ,sp_t_SC107100_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_SC107100_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP27100_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_SCP27100_merge]"]]}
            ,sp_t_SCP37100_merge:{build job: 'PSTA_ISCALA_71_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_71].[sp_t_SCP37100_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_71
    }
}
def function_PSTA_ISCALA_72() {
    stage('PSTA_ISCALA_72')
    {
        def PSTA_ISCALA_72 = [
             sp_t_GL0372YY_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_GL0372YY_merge]"]]}
            ,sp_t_MP617200_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_MP617200_merge]"]]}
            ,sp_t_SC017200_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_SC017200_merge]"]]}
            ,sp_t_SC037200_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_SC037200_merge]"]]}
            ,sp_t_SC107200_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_SC107200_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP27200_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_SCP27200_merge]"]]}
            ,sp_t_SCP37200_merge:{build job: 'PSTA_ISCALA_72_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_72].[sp_t_SCP37200_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_72
    }
}
def function_PSTA_ISCALA_74() {
    stage('PSTA_ISCALA_74')
    {
       def PSTA_ISCALA_74 = [
             sp_t_GL0374YY_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_GL0374YY_merge]"]]}
            ,sp_t_MP617400_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_MP617400_merge]"]]}
            ,sp_t_SC017400_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_SC017400_merge]"]]}
            ,sp_t_SC037400_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_SC037400_merge]"]]}
            ,sp_t_SC107400_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_SC107400_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP27400_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_SCP27400_merge]"]]}
            ,sp_t_SCP37400_merge:{build job: 'PSTA_ISCALA_74_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_74].[sp_t_SCP37400_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_74
    }
}
def function_PSTA_ISCALA_77() {
    stage('PSTA_ISCALA_77')
    {
        def PSTA_ISCALA_77 = [
             sp_t_GL0377YY_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_GL0377YY_merge]"]]}
            ,sp_t_MP617700_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_MP617700_merge]"]]}
            ,sp_t_SC017700_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_SC017700_merge]"]]}
            ,sp_t_SC037700_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_SC037700_merge]"]]}
            ,sp_t_SC107700_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_SC107700_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP27700_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_SCP27700_merge]"]]}
            ,sp_t_SCP37700_merge:{build job: 'PSTA_ISCALA_77_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_77].[sp_t_SCP37700_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_77
    }
}
def function_PSTA_ISCALA_79() {
    stage('PSTA_ISCALA_79')
    {
        def PSTA_ISCALA_79 = [
             sp_t_GL0379YY_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_GL0379YY_merge]"]]}
            ,sp_t_MP617900_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_MP617900_merge]"]]}
            ,sp_t_SC017900_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_SC017900_merge]"]]}
            ,sp_t_SC037900_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_SC037900_merge]"]]}
            ,sp_t_SC107900_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_SC107900_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP27900_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_SCP27900_merge]"]]}
            ,sp_t_SCP37900_merge:{build job: 'PSTA_ISCALA_79_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_79].[sp_t_SCP37900_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_79
    }
}
def function_PSTA_ISCALA_86() {
    stage('PSTA_ISCALA_86')
    {
        def PSTA_ISCALA_86 = [
             sp_t_GL0386YY_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_GL0386YY_merge]"]]}
            ,sp_t_MP618600_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_MP618600_merge]"]]}
            ,sp_t_SC018600_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_SC018600_merge]"]]}
            ,sp_t_SC038600_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_SC038600_merge]"]]}
            ,sp_t_SC108600_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_SC108600_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_ScaCompanySegment_merge]"]]}
           ,sp_t_SCP28600_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_SCP28600_merge]"]]}
            ,sp_t_SCP38600_merge:{build job: 'PSTA_ISCALA_86_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_86].[sp_t_SCP38600_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_86
    }
}
def function_PSTA_ISCALA_94() {
    stage('PSTA_ISCALA_94')
    {
        def PSTA_ISCALA_94 = [
             sp_t_GL0394YY_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_GL0394YY_merge]"]]}
            ,sp_t_MP619400_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_MP619400_merge]"]]}
            ,sp_t_SC019400_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_SC019400_merge]"]]}
            ,sp_t_SC039400_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_SC039400_merge]"]]}
            ,sp_t_SC109400_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_SC109400_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP29400_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_SCP29400_merge]"]]}
            ,sp_t_SCP39400_merge:{build job: 'PSTA_ISCALA_94_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_94].[sp_t_SCP39400_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_94
    }
}
def function_PSTA_ISCALA_A1() {
    stage('PSTA_ISCALA_A1')
    {
        def PSTA_ISCALA_A1 = [
             sp_t_GL03A1YY_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_GL03A1YY_merge]"]]}
            ,sp_t_MP61A100_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_MP61A100_merge]"]]}
            ,sp_t_SC01A100_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_SC01A100_merge]"]]}
            ,sp_t_SC03A100_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_SC03A100_merge]"]]}
            ,sp_t_SC10A100_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_SC10A100_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP2A100_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_SCP2A100_merge]"]]}
            ,sp_t_SCP3A100_merge:{build job: 'PSTA_ISCALA_A1_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_A1].[sp_t_SCP3A100_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_A1
    }
}
def function_PSTA_ISCALA_YA() {
    stage('PSTA_ISCALA_YA')
    {
        def PSTA_ISCALA_YA = [
             sp_t_GL03YAYY_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_GL03YAYY_merge]"]]}
            ,sp_t_MP61YA00_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_MP61YA00_merge]"]]}
            ,sp_t_SC01YA00_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_SC01YA00_merge]"]]}
            ,sp_t_SC03YA00_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_SC03YA00_merge]"]]}
            ,sp_t_SC10YA00_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_SC10YA00_merge]"]]}
            ,sp_t_ScaCompanySegment_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_ScaCompanySegment_merge]"]]}
            ,sp_t_SCP2YA00_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_SCP2YA00_merge]"]]}
            ,sp_t_SCP3YA00_merge:{build job: 'PSTA_ISCALA_YA_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_ISCALA_YA].[sp_t_SCP3YA00_merge]"]]}
 
        ]
        parallel PSTA_ISCALA_YA
    }
}
def function_PSTA_SAP() {
    stage('PSTA_SAP')
    {
        def PSTA_SAP = [
             sp_t_MAKT_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_MAKT_merge]"]]}
            ,sp_t_MARA_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_MARA_merge]"]]}
            ,sp_t_MARC_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_MARC_merge]"]]}
            ,sp_t_MAST_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_MAST_merge]"]]}
            ,sp_t_MVKE_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_MVKE_merge]"]]}
            ,sp_t_STAS_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_STAS_merge]"]]}
            ,sp_t_STKO_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_STKO_merge]"]]}
            ,sp_t_STPO_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_STPO_merge]"]]}
            ,sp_t_STPU_merge:{build job: 'PSTA_SAP_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_SAP].[sp_t_STPU_merge]"]]}
 
        ]
        parallel PSTA_SAP
    }
}
def function_PSTA_TIS() {
    stage('PSTA_TIS')
    {
        def PSTA_TIS = [
             sp_t_JH_EDV_SYSTEM_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_JH_EDV_SYSTEM_merge]"]]}
            ,sp_t_T_CHK_STA_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_CHK_STA_merge]"]]}
            ,sp_t_T_D4S_STAT_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_D4S_STAT_merge]"]]}
            ,sp_t_T_EWO_DAT_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_EWO_DAT_merge]"]]}
            ,sp_t_T_MASTER_DAT_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_MASTER_DAT_merge]"]]}
            ,sp_t_T_MASTER_ORG_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_MASTER_ORG_merge]"]]}
            ,sp_t_T_MASTER_STR_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_MASTER_STR_merge]"]]}
            ,sp_t_T_MPI_DAT_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_MPI_DAT_merge]"]]}
            ,sp_t_T_ORG_DAT_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_ORG_DAT_merge]"]]}
            ,sp_t_T_ORG_SYS_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_ORG_SYS_merge]"]]}
            ,sp_t_T_WRK_SET_DAT_merge:{build job: 'PSTA_TIS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[PSTA_TIS].[sp_t_T_WRK_SET_DAT_merge]"]]}
 
        ]
        parallel PSTA_TIS
    }
}
def function_STA_MDS() {
    stage('STA_MDS')
    {
        def STA_MDS = [
             UnpivotPlanOccupancyTimeKW:{build job: 'STA_MDS_with_Parameter',parameters: [[$class: 'StringParameterValue', name: 'p_STORED_PROCEDURE_NAME', value: "[STA_MDS].[UnpivotPlanOccupancyTimeKW]"]]}
 
        ]
        parallel STA_MDS
    }
}
