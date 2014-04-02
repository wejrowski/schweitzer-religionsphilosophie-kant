
task :split do
  lines_per_page = 400

  @current_page = 0
  line_num = 0
  waiting = false

  set_headers

  File.open('source/_posts/all.markdown').each do |line|
    line_num += 1

    File.open(curr_filename, 'a').puts line

    if line_num >= lines_per_page
      waiting = true
    end

    if waiting && reached_split_point?(line)
      @current_page += 1
      set_headers

      puts "SPLIT: " + curr_filename
      line_num = 0
      waiting = false
    end
    @last_line = line

  end

end

def reached_split_point?(line)
  (@last_line == "\n" && line == "\n")
end

def last_line_was_blank?
  @last_line == "\n"
end

def curr_filename
  i = "%04d" % @current_page
  "source/_posts/german-#{i}.markdown"
end

def set_headers
  f = File.open(curr_filename, 'a')
  f.puts '---'
  f.puts 'layout: german'
  f.puts "title: Albert Schweitzer - Die Religionspbilosophie Kant's - #{@current_page}"
  f.puts 'category: german'
  f.puts '---'
end
