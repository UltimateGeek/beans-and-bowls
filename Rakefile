NAME="Beans___Bowls"

task :vtt do |t|
    sh "rm -f #{NAME}.vtt"
    Dir.chdir('src/vtt') do
        sh "zip -D ../../#{NAME}.vtt *.json"
    end
end

task :package => [:vtt]

task :default => :package


VTT_JSON_FILE="jaa6.json"
VTT_ROOM_ID="beansandbowls"
VTT_SERVER_URL="https://localhost:8272"

task :push_vtt do |t|
  sh "curl -X PUT -H 'Content-Type: application/json' --data-binary '@src/vtt/#{VTT_JSON_FILE}' #{VTT_SERVER_URL}/state/#{VTT_ROOM_ID}"
end

task :push => :push_vtt

TMP_DIR = "#{ENV['HOME']}/Downloads"

task :extract_vtt do |t|
    tmp_file = "#{NAME}.vtt"
    if (File.exist?("#{TMP_DIR}/#{tmp_file}"))
        json_file = VTT_JSON_FILE
        Dir.chdir(TMP_DIR) do
            sh "rm -f #{json_file}"
            sh "unzip #{tmp_file}"
        end
        sh "cp #{TMP_DIR}/#{json_file} src/vtt/#{json_file}"
        sh "echo "" >> src/vtt/#{json_file}"
        sh "rm #{TMP_DIR}/#{tmp_file}"
    end
end

task :extract => [:extract_vtt]
