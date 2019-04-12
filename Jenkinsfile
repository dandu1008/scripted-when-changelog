node {
    checkout([$class: 'GitSCM', 
				branches: [[name: "origin/master"]], 
				userRemoteConfigs: [[
                url: 'https://github.com/dandu1008/scripted-when-changelog.git']],
				])
	def changeLogFound = false
	def changeLogSets = currentBuild.changeSets
	println "changeLogSets: ${changeLogSets}"
	println "changeLogSets.size(): ${changeLogSets.size()}"
	
	for (i = 0; i < changeLogSets.size(); i++) {
	    println changeLogSets[i].getClass().getName()
	    
	    def entries = changeLogSets[i].items
	    for (j = 0; j < entries.length; j++) {
	        def entry = entries[j]
	        println "${entry}"
	        println "${entry.msg}"
	        if (entry.msg =~ /.*some_text.*/) {
	            changeLogFound = true
	            break;
	        } 
	    }
	    
	    if (changeLogFound)
	       break
	}
	
	changeLogSets = null
	
	if (changeLogFound) {
	    stage('changeLogFound') {
	        echo 'Change log is found'
	    }
	}
	else {
	    stage('changeLogNotFound') {
	        echo 'Change log is not found'
	    }
	}
}
