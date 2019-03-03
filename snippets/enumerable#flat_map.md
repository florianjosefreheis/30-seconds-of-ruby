Enumerable#flat_map
When dealing with relational data, sometimes we need to collect a bunch of unrelated attributes and return them in an array that is not nested. Let’s imagine you had a blog application, and you wanted to find the authors of comments left on posts written in the last month by a given set of users.

You might do something like this:
module CommentFinder
  def self.find_for_users(user_ids)
    users = User.where(id: user_ids)
    users.map do |user|
      user.posts.map do |post|
        post.comments.map |comment|
          comment.author.username
        end
      end
    end
  end
end
You would then end up with a result such as:
[[['Ben', 'Sam', 'David'], ['Keith']], [[], [nil]], [['Chris'], []]]
I know, I know. You just wanted the authors! Here, we'll call flatten.
module CommentFinder
  def self.find_for_users(user_ids)
    users = User.where(id: user_ids)
    users.map { |user|
      user.posts.map { |post|
        post.comments.map { |comment|
          comment.author.username
        }.flatten
      }.flatten
    }.flatten
  end
end
Another option would have been to use flat_map, which does the flattening as you go:
module CommentFinder
  def self.find_for_users(user_ids)
    users = User.where(id: user_ids)
    users.flat_map { |user|
      user.posts.flat_map { |post|
        post.comments.flat_map { |comment|
          comment.author.username
        }
      }
    }
  end
end
It’s not too much different but better than having to call flatten a bunch of times.
